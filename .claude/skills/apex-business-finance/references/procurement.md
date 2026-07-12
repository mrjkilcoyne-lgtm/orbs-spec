# Procurement

## Scope
Managing vendor relationships and purchasing processes: sourcing, negotiation, contract management, and spend control.

## Core principles
- Procurement is about total cost of ownership (TCO), not just unit price; if a 20% cheaper vendor requires 30% more time to support, the deal is worse.
- Vendor concentration risk (reliance on one supplier) is a liability; prefer 2-3 vetted vendors per category to prevent hostage-taking when renegotiating.
- Strategic vs. transactional spend require different approaches: strategic spend (infrastructure, core vendors) requires long-term relationships and deep negotiation; transactional spend (office supplies, one-off services) should be automated and minimized.
- Volume leverage is real; consolidating spend across multiple categories with one vendor can unlock 10-20% discounts (Salesforce + Slack bundling, AWS bundling).
- Procurement governance (approval workflows by spend category and amount) prevents maverick buying (teams buying without standards) but adds friction; scale governance with company size.

## Apex practices
- Standardize vendor selection criteria (SLA uptime, support response time, data residency, security certification) and publish them; this prevents repeated negotiations on non-negotiable items.
- Implement a strategic sourcing process quarterly: analyze spend, identify savings opportunities, batch similar requests, and negotiate volume discounts.
- Build a vendor scorecard (on-time delivery, quality, support responsiveness, invoicing accuracy) and share it with vendors; transparency improves performance and makes contract renewal conversations data-driven.
- Automate low-value spending (corporate cards, approved vendors, category approval limits) so procurement can focus on strategic negotiations.

## Pitfalls
- Selecting vendors on lowest price without regard to TCO; a cheaper cloud provider that requires 2x engineering time for integration is more expensive.
- Single-vendor lock-in; if one vendor becomes critical, you forfeit negotiating leverage and they know it.
- Treating all vendor relationships the same way; a critical vendor relationship requires relationship investment (quarterly business reviews, shared roadmaps), while transactional vendors need automated reordering.

## Tools & references
Coupa, Ariba (SAP), Jaggr (spend analytics), Request for Proposal (RFP) templates, APICS procurement standards, negotiation frameworks (Fisher & Ury), Gartner magic quadrants for vendor comparison.
