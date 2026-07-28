# Unknown Unknowns

## Scope
The risks not on the risk list: surfacing what you don't know you don't know — in plans, designs, and mental models of systems.

## Core principles
- The Johari expansion: known knowns, known unknowns (you can schedule research), unknown knowns (tacit assumptions you could surface), unknown unknowns (invisible until they hit) — the last two are attacked indirectly, by process, not by staring harder.
- Unknown unknowns cluster at boundaries: between systems (integration points), between teams (assumed ownership), between abstraction layers (what the ORM actually emits), and outside your experience base — the map has edges exactly where you've never been.
- Assumptions are unknowns in disguise: every plan encodes dozens of unstated "of courses" (the API is stable, the data is clean, the user has one account); listing them converts unknown-knowns into checkable claims — the cheapest de-risking available.
- Diversity of vantage is the only broad-spectrum detector: the new hire, the adjacent-domain expert, and the actual user each see a different blind region of yours; soliciting them is not politeness, it's instrumentation.
- Exploration must be budgeted, not hoped for: spikes, prototypes, and chaos experiments exist to make unknowns announce themselves in a sandbox instead of in production.

## Detection tests
- What am I assuming so deeply I didn't write it down? (Force the assumptions list; the embarrassing entries are the valuable ones.)
- Where does my plan touch territory I've literally never operated in?
- Who would find this plan naive, and have they seen it?

## Countermeasures
- Premortem specifically for surprise: "it failed for a reason none of us listed today — what was it?" pushes past the known-risk register.
- Prototype the riskiest integration first (walking skeleton): end-to-end thin slices flush boundary unknowns early while change is cheap.
- Timebox raw exploration in new territory before estimating it — you cannot size a space you haven't entered.

## Tools & references
Johari window, Rumsfeld matrix (used seriously), walking-skeleton pattern, chaos engineering, "The Field Guide to Understanding Human Error" (Dekker).
