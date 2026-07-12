# Technical SEO

## Scope
Making sites crawlable, indexable, and well-represented in search — the engineering side.

## Core principles
- Crawl → render → index → rank: diagnose problems in pipeline order; a page that isn't crawled can't rank.
- One canonical URL per piece of content: redirects, rel=canonical, and consistent internal links defend it.
- Content in the HTML wins: SSR/SSG for anything that must rank; client-rendered content gets second-pass rendering at best.
- Metadata is the contract: title/meta description influence clicks; structured data (JSON-LD) unlocks rich results.
- Site architecture is ranking plumbing: internal links distribute authority; orphan pages effectively don't exist.

## Apex practices
- Maintain XML sitemaps + robots.txt deliberately; verify with Search Console coverage reports, not assumptions.
- Ship correct status codes: 404 for gone, 301 for moved, no soft-404s (200 "not found" pages).
- Core Web Vitals as tiebreaker: fast pages win close calls; fix p75 field data.
- Audit renderability: fetch as Google (URL inspection), check what the crawler sees vs users.

## Pitfalls
- Infinite URL spaces (filters, session params) burning crawl budget — canonicalize and block.
- hreflang/canonical conflicts sending mixed signals.
- JS-only navigation invisible to crawlers (real <a href> links matter).

## Tools & references
Google Search Console, Screaming Frog, schema.org + Rich Results Test, Ahrefs/Semrush for the market view.
