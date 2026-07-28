# Supply-Chain Security

## Scope
Securing everything upstream of your code in production: third-party dependencies, build pipelines, artifacts, and the integrity chain from source to deploy.

## Core principles
- Your attack surface is your transitive closure: a typical app directly declares dozens of packages and inherits thousands; each maintainer account, build server, and registry in that graph is your perimeter (left-pad showed fragility; event-stream, SolarWinds, and xz-utils showed hostility).
- Version pinning with lockfiles and checksum verification is the foundation: floating ranges mean your build installs whatever the registry serves that day — the exact mechanism of dependency-confusion attacks (Birsan's 2021 research: internal package names squatted publicly with higher versions).
- The build system is a production system: SLSA levels formalize this — provenance generation (L1), hosted hardened builders (L2-L3), so an artifact can prove which source and workflow produced it; unsigned artifacts from a laptop are unverifiable by construction.
- Malicious packages ≠ vulnerable packages: CVE scanning catches known-vulnerable code, but install-script malware, typosquats, and maintainer-account takeovers need behavioral signals (new maintainer, install hooks, obfuscated blobs, sudden network calls) — different tools, different feeds.
- SBOMs make incident response tractable: when the next Log4Shell drops, "which of our 400 services ships log4j-core between 2.0 and 2.14.1" must be a query (minutes), not an archaeology project (weeks).

## Apex practices
- Generate SBOMs (CycloneDX/SPDX via Syft) at build time, store them queryably (Dependency-Track/GUAC), and sign artifacts + attestations with Sigstore cosign; verify signatures at deploy admission.
- Quarantine new dependencies and new versions: a cooldown period (e.g., no versions younger than 72 hours) plus review of install scripts and diffs — most malicious versions are detected and yanked within days.
- Kill dependency confusion structurally: scoped/namespaced internal packages, registry configuration that never falls through to public for internal names, and claim your internal names on public registries.
- Harden CI: pin GitHub Actions to full commit SHAs (tags are mutable), scope tokens per-job with least privilege, isolate build steps, and require provenance for anything deployed.

## Pitfalls
- Trusting `npm audit`-style output as the whole picture while `postinstall` scripts run arbitrary code at developer-laptop privilege on every install.
- Vendoring or forking dependencies to "control" them, then never pulling upstream security patches — you've traded supply-chain risk for guaranteed staleness.
- Signing artifacts but never verifying signatures at admission — an unverified signature chain is a decorative one.

## Tools & references
SLSA framework, Sigstore (cosign/Fulcio/Rekor), Syft/Grype, CycloneDX & SPDX, OWASP Dependency-Track, OpenSSF Scorecard, deps.dev, NIST SSDF (SP 800-218), Renovate/Dependabot.
