### To extract json keys from a column in sql we can use following syntax

In following example we are querying column meta_date of table products and we are trying to fetch review & discount keys from meta_date column

```sql
SELECT JSON_EXTRACT(meta_data, '$.review') AS productReview,
JSON_EXTRACT(meta_data, '$.discount') AS currentDiscount
FROM products
WHERE product_id = 1

```
