# Filesystems

## Scope
Linux filesystems and the VFS layer: ext4/XFS/Btrfs/ZFS semantics, journaling, durability (fsync), inodes and directories, and storage behavior applications depend on.

## Core principles
- Durability is opt-in: write() puts data in the page cache; only fsync/fdatasync (on the file AND, for new files, the containing directory) makes it survive power loss. The "crash-consistent rename" pattern — write temp, fsync temp, rename, fsync dir — is the portable atomic-update recipe.
- fsync failure is not retryable: after an fsync error, dirty pages may be marked clean without reaching disk; retrying fsync can return success while data is gone (the 2018 PostgreSQL "fsyncgate" — the correct response is to treat the write as lost, e.g., crash and recover from WAL).
- Journaling protects metadata, not necessarily your data: ext4's default `data=ordered` writes data before committing metadata, preventing garbage-in-files but not guaranteeing your application-level consistency; only fsync ordering gives you that.
- Inodes are the identity, names are references: hard links share an inode, a file deleted while open lives until the last fd closes (why "df says full, du disagrees" — check `lsof +L1`), and inode exhaustion (`df -i`) fails writes on a disk with free space.
- Filesystems differ where it hurts: ext4 is the balanced default; XFS excels at parallel large-file I/O and huge directories; Btrfs/ZFS add CoW snapshots, checksums, and send/receive but have different performance envelopes (CoW + databases needs `nodatacow` or tuned recordsize). O_DIRECT, fallocate, and reflink support vary — verify per-fs.

## Apex practices
- State your durability contract explicitly in code review: which writes are fsynced, in what order, and what crash-recovery replays — then test it with power-fail simulation (dm-log-writes, CrashMonkey/ALICE) rather than hoping.
- Watch the real limits: `df -h` and `df -i`, directory entry counts (millions of files in one dir degrade lookup on ext4 without dir_index tuning; prefer hashed subdirectory fanout), and open-fd leaks holding deleted files.
- Choose mount options from evidence: `noatime` (or default relatime) to kill read-triggered writes; for ZFS/Btrfs match recordsize/compression to workload (16 KB recordsize for Postgres, zstd compression for logs).
- Use fio for storage truth: measure the actual device with the workload's block size, queue depth, and sync flags before blaming the filesystem — many "filesystem slow" reports are `fsync`-heavy workloads on high-latency cloud disks (EBS gp3 ~1 ms fsync vs local NVMe ~20 µs).

## Pitfalls
- Assuming rename is enough without the fsyncs: after crash, a rename-without-fsync can yield a zero-length file (the infamous ext4 O_PONIES debate) — applications lost real data to this.
- Treating network filesystems as local: NFS close-to-open consistency, no reliable locking without care (flock over NFS), and hung-mount D-states that block reboots; SQLite over NFS is a documented corruption recipe.
- Ignoring write amplification interactions: databases on CoW filesystems, or small random writes on RAID5/parity storage, multiply physical I/O several-fold — the workload/storage pairing, not either alone, determines performance.

## Tools & references
"The Linux Programming Interface" ch. 13-14 (Kerrisk), ext4/XFS/Btrfs kernel docs, PostgreSQL fsyncgate writeups, ALICE/CrashMonkey papers (OSDI); fio, blktrace/biosnoop, df/du/lsof, xfs_io, e2fsprogs.
