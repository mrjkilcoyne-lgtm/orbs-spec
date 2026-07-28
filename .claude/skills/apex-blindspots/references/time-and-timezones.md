# Time & Timezones

## Scope
The blindspot family around dates, times, zones, DST, and calendars — where confident code silently corrupts schedules, bills, and analytics.

## Core principles
- A timestamp and a wall-clock time are different types: "2026-03-08 02:30" in New York doesn't exist (DST spring-forward) and "01:30" happens twice in fall — instants (UTC points) vs local times (zone-dependent projections) must never share a variable.
- Store instants in UTC, but future events in local time + zone: "meeting at 9am Paris next June" must survive Paris changing its DST rules — storing it as UTC bakes in today's offset and breaks on rule changes (the classic calendar-app corruption).
- Offsets are not zones: +02:00 is a moment's arithmetic; Europe/Paris is a political history with different offsets across the year and across decades — serialize the IANA zone name, not the offset, when the zone matters.
- Durations vs periods: 24 hours after 23:00 on DST night is not "the same time tomorrow"; adding a day is calendar math, adding 86400 seconds is physics — libraries separate these (Duration vs Period) because conflating them double-bills customers twice a year.
- The day boundary is a per-zone fiction: "daily" aggregates, "today's" orders, birthday checks — each needs an explicit zone decision; UTC-midnight buckets shift a Sydney business's Monday sales into Sunday's report.

## Detection tests
- For each datetime in the system: is it an instant or a local time, and does its storage type say so?
- What happens to this code on DST-transition night, at year boundary, on Feb 29?
- Whose midnight defines "today" in every daily job, report, and rate-limit window?

## Countermeasures
- Use the modern library (java.time, Temporal, chrono, zoneinfo) and its distinct types; hand-rolled offset math is a defect with a delay timer.
- Test with the cursed fixtures: DST transitions both directions, Feb 29, week 53, zones like Asia/Kathmandu (+05:45) and Pacific/Chatham (+12:45), and a pre-1970 date.
- Pin server/CI/database session zones to UTC explicitly so environment defaults can't reshuffle results between laptop and prod.

## Tools & references
IANA tzdb, "Falsehoods programmers believe about time," java.time / JS Temporal design docs, Jon Skeet's timezone writings.
