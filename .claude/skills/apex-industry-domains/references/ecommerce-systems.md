# Ecommerce Systems

## Scope
Online marketplaces and retail: catalog management, inventory, orders, fulfillment, payments, and customer experience at scale.

## Core principles
- Inventory is the core constraint: every unit sold must be tracked, reserved, and shipped or canceled; overselling causes customer anger and refund complexity.
- Catalog scale is non-trivial: millions of SKUs, variants (size, color), pricing rules, promotions, and availability vary by region and time; the data model determines query speed.
- Customer conversion is rate-limited: every friction point (page load, checkout steps, shipping cost surprise) loses customers; performance and clarity are revenue drivers.
- Fulfillment is supply-chain: pick-pack-ship must be efficient; returns are costly; the physical flow of goods shapes the entire business model.
- Pricing is dynamic and regulated: discounts, taxes, shipping, and currency conversion vary by location, promotion, and inventory; incorrect pricing is both fraud risk and customer-satisfaction killer.

## Apex practices
- Use transactional inventory: on order creation, reserve inventory (lock it from sale), then confirm shipment; overselling is a bug, not a feature.
- Cache heavily but invalidate carefully: product catalogs change (price, availability), but invalidating every product on stock change kills caches; use partial invalidation.
- Implement shipping carrier integrations (FedEx, UPS, USPS, DHL) for rate and label generation; hardcoding shipping cost guarantees rework.
- Design returns handling upfront: restocking logic, refund processing, and warranty handling are complex; a returns system designed later is expensive.

## Pitfalls
- Overselling due to race conditions between inventory check and order creation; require pessimistic locking (lock inventory row during order).
- Underselling by over-reserving: if abandoned carts hold inventory forever, available inventory shrinks artificially.
- Ignoring tax complexity: sales tax, VAT, and tariffs are territorial and change frequently; manual calculation ensures failures.

## Tools & references
Shopify, WooCommerce, Magento (legacy), custom (Stripe, Adyen for payments), inventory management (NetSuite, SAP), carrier APIs (FedEx Developer, UPS onsite).
