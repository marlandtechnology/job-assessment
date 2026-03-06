# Assessment
Assignment is to transform Marketplace into STAR schema with core calculations: top seller, top products, top customer location
Use DBT to model the data and create a new repo and submit the DBT project for review in a public repo.


Core Tables (Entities)

    customer: Stores primary user profiles.

        Fields: customer_id (PK), first_name, last_name, email (Unique), created_at.

    customer_address: A localized table allowing customers to store multiple shipping locations.

        Fields: address_id (PK), customer_id (FK), address_line_1, city, state, zip_code, is_default_shipping.

    seller: Details for third-party vendors or internal storefronts.

        Fields: seller_id (PK), store_name, rating, joined_date.

    product: The master catalog of items available for sale.

        Fields: product_id (PK), product_name, category, brand.

Bridge Tables (Inventory)

    seller_product_price: Maps products to specific sellers, managing the "Listing" price and live stock levels.

        Fields: seller_id (FK), product_id (FK), current_price, stock_quantity, updated_at.

        Note: Uses a composite Primary Key on seller_id and product_id.

Transaction Tables (Sales)

    ORDER: The header record for a purchase, capturing the "who," "where," and "total."

        Fields: order_id (PK), customer_id (FK), shipping_address_id (FK), order_date, total_order_amount, status.

    order_line: The line-item detail for every unique product/seller combination within an order.

        Fields: order_line_id (PK), order_id (FK), product_id (FK), seller_id (FK), quantity, unit_price_at_sale, line_total
