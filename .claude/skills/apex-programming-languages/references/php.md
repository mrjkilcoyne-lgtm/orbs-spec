# PHP

## Scope
Modern PHP (8.x): typed properties, the request lifecycle, Composer ecosystem.

## Core principles
- Modern PHP is typed: declare(strict_types=1), typed properties, enums, readonly — the loose PHP of folklore is opt-out.
- Share-nothing request model: each request starts clean; state lives in DB/cache, which shapes all architecture.
- Composer + PSR standards (PSR-4 autoload, PSR-12 style, PSR-7/15 HTTP) define the ecosystem's grain.
- The framework (Laravel/Symfony) is the platform: DI containers, middleware, and ORM conventions matter more than raw PHP.
- Escape output per context (HTML/attr/URL/SQL via prepared statements) — injection is still the #1 PHP wound.

## Apex practices
- Prepared statements always (PDO); never string-build queries.
- Value objects + enums for domain modeling; avoid arrays-as-structs in new code (use readonly classes/DTOs).
- Static analysis at max level (PHPStan/Psalm) — it transforms PHP reliability.
- Use FrankenPHP/OPcache/preloading knowledge for performance rather than folklore micro-tweaks.

## Pitfalls
- Loose comparison (`==`) type-juggling surprises; always `===`.
- Suppressing errors with `@` instead of handling them.
- Mixing template logic and business logic in one file (the legacy trap).

## Tools & references
PHPStan, PHP-CS-Fixer, PHPUnit/Pest, Laravel/Symfony docs, phptherightway.com.
