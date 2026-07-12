# Bash & Shell Scripting

## Scope
Robust POSIX/Bash scripting: quoting, error handling, composition of Unix tools.

## Core principles
- Quote every expansion (`"$var"`) — word splitting and globbing on unquoted vars is the root of most shell bugs.
- `set -euo pipefail` as the baseline; know its gaps (conditions, command substitution) rather than trusting it blindly.
- A script is glue: once it grows functions-calling-functions with data structures, switch to Python/Go.
- Exit codes are the API: 0 success, non-zero meaningful; check them or chain with `&&`/`||` deliberately.
- Prefer `$(...)` over backticks, `[[ ]]` over `[ ]`, arrays over space-separated strings in Bash.

## Apex practices
- shellcheck on every script, in CI — it catches the entire folklore bug catalog mechanically.
- Use `trap` for cleanup (tempfiles, background jobs) on EXIT/INT/TERM.
- `mktemp` for temp files, `printf` over `echo` for portability, `--` to end option parsing before user input.
- Make scripts re-runnable (idempotent) and safe under `set -x` (no secrets in commands).

## Pitfalls
- Parsing `ls` output; iterate globs or use `find -print0 | xargs -0`.
- `cd` without checking failure, then operating in the wrong directory.
- Pipelines swallowing failures without pipefail; `cmd | head` SIGPIPE surprises.

## Tools & references
shellcheck, shfmt, Google Shell Style Guide, BashFAQ (mywiki.wooledge.org).
