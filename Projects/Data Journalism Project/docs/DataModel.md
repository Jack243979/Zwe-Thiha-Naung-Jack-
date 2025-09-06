# Data Model & Relationships

Central fact: **order_items**
- Keys: `order_id`, `product_id`

Relationships
- `order_items` → `orders` on `order_id`
- `orders` → `customers` on `customer_id`
- `orders` → `stores` on `store_id`
- `order_items` → `products` on `product_id`
- `products` → `categories` on `category_id`
- `products` → `brands` on `brand_id`
- `products` → `stocks` on `product_id`
- `stocks` → `store-stocks` (if present) on `store_id` + `product_id`

Notes
- Use **Relationships** (not rigid joins) so Tableau pushes joins at viz time.
- When filtering by **Map/State**, prefer **context filters** or “Apply to selected worksheets” to avoid granularity inflation on Top-N charts.
