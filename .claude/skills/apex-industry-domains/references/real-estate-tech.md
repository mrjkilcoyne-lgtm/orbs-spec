# Real Estate Tech

## Scope
Property management, valuation, transaction platforms, and spatial data: listing data, pricing models, escrow/title, and geographic search.

## Core principles
- Property data is locational: every property is unique by address and characteristics (structure, amenities, history), requiring custom appraisal and valuation modeling.
- Pricing depends on comps (comparable sales): recent sales of similar properties nearby inform value; hedonic pricing models weight characteristics (square footage, bedrooms, pool, school district, proximity to transit).
- Transaction legality is complex: title (ownership proof), liens, contingencies (appraisal, inspection, financing), and state/local requirements vary; transaction platforms are heavily regulated.
- Geographic search (find properties near X within Y miles) requires geospatial indexing (R-tree, quadtree, or PostGIS); naive radius queries are slow.
- Escrow and title insurance are trust layers: buyers need assurance that title is clear, seller needs assurance of payment, lender needs security; systems coordinate these.

## Apex practices
- Integrate public records (MLS, county assessor, deed recordings): real-time data beats cached data; APIs differ by county/state, making aggregation complex.
- Use geospatial databases (PostGIS, MongoDB geospatial, Elasticsearch) for location-based queries; they're worth the operational complexity.
- Build valuation models (Zillow-style "Zestimate") using machine learning (LightGBM, XGBoost) on historical transactions and property features; models degrade without retraining.
- Separate transaction workflow from listing: a property can be listed, offered, inspected, appraised, financed, and closed over months; state machines model transitions.

## Pitfalls
- Assuming transaction data is accurate; deeds record what happened, but math errors, typos, and misfilings are common in historical records.
- Relying on single-vendor MLS data; missing non-MLS sales (private, cash) biases valuation models.
- Treating square footage as truth; older properties often have no recorded footage, and measurements vary by method (gross, net, heated).

## Tools & references
MLS platforms (Zillow, Redfin, Trulia), county assessor records (varies by state), Redfin/Zillow data APIs, PostGIS (geospatial), tax assessment databases, title companies, appraisal standards (USPAP).
