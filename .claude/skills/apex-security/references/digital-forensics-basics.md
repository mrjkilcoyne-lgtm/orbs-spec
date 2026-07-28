# Digital Forensics Basics

## Scope
Acquiring, preserving, and analyzing digital evidence to reconstruct what happened — for internal investigations and incident response, with integrity that survives scrutiny.

## Core principles
- Order of volatility governs acquisition sequence (RFC 3227): registers/cache → memory → network state → running processes → disk → logs/backups; capture the most ephemeral first, because every action you take destroys volatile state.
- Never work on originals: acquire a forensic image (bit-for-bit, write-blocked for physical media; snapshots for cloud volumes), hash it (SHA-256) at acquisition, and analyze copies — the hash chain is what makes your findings reproducible and defensible.
- Chain of custody is a discipline, not paperwork: who acquired what, when, from where, with what tool and hash, and every transfer since — an evidence gap turns "we know" into "we believe" for legal, HR, or insurance purposes.
- Timeline reconstruction is the core analytical method: normalize timestamps (to UTC, noting clock skew) across filesystem metadata (MACB times), event logs, shell histories, browser artifacts, and cloud audit trails into one super-timeline — correlation across sources is what exposes the story.
- Absence of evidence is evidence of limits, not innocence: attackers use timestomping, log deletion, and living-off-the-land binaries (LOLBins) that leave minimal traces; your conclusions must state confidence and what could not be determined.

## Apex practices
- Memory-capture first on live systems (before pulling power or isolating): process lists, network connections, injected code, and encryption keys exist only in RAM — Volatility-analyzable memory is often the whole case.
- In cloud environments, forensics is API-driven: snapshot EBS/PD volumes, export CloudTrail/audit logs immediately (before retention windows lapse), preserve serial-console output, and tag+lock evidence resources against lifecycle deletion.
- Know the high-yield artifacts per OS: Windows — event logs, prefetch, ShimCache/Amcache, registry hives, $MFT/USN journal; Linux — auth.log/journald, shell histories, cron, /proc for live systems, auditd; plus browser profiles and cloud-agent logs everywhere.
- Automate triage collection with tools like Velociraptor or KAPE so responders grab a consistent artifact bundle in minutes, then decide what merits full imaging.

## Pitfalls
- "Just looking around" on a live compromised box — every command updates access times, overwrites memory, and can trip attacker tripwires; collection must be deliberate and logged.
- Trusting timestamps naively: timezone confusion, clock drift, and deliberate timestomping ($STANDARD_INFORMATION vs $FILE_NAME time mismatches on NTFS are the tell).
- Letting infrastructure automation destroy evidence — autoscaling terminates the compromised instance, log rotation eats the window, CI re-images the box; place preservation holds within the first hour.

## Tools & references
RFC 3227, NIST SP 800-86, Volatility 3, Autopsy/Sleuth Kit, Velociraptor, KAPE, plaso/log2timeline, FTK Imager, SANS DFIR posters and FOR500/FOR508 curricula.
