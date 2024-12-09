Fetch all the physical items ordered in the month of September 2023.
```
select
	oi.order_id,
	oi.order_item_seq_id,
	p.PRODUCT_ID,
	p.PRODUCT_NAME,
	p.PRODUCT_TYPE_ID,
	p.BRAND_NAME,
	oi.STATUS_ID,
	os.STATUS_DATETIME,
	pt.is_physical
from
	order_item oi
join order_status os on
	oi.ORDER_ID = os.ORDER_ID
	and oi.ORDER_ITEM_SEQ_ID = os.ORDER_ITEM_SEQ_ID
	and oi.STATUS_ID = 'ITEM_CREATED'
	and oi.STATUS_ID = os.STATUS_ID
join product p on
	oi.product_id = p.PRODUCT_ID
join product_type pt on
	pt.product_type_id = p.PRODUCT_TYPE_ID
	and is_physical = 'y'
where
	extract(year from os.STATUS_DATETIME) = "2023"
	and extract(month from os.STATUS_DATETIME) = '09';
```
Alternative solution 
```
SELECT
	oi.order_id,
	oi.order_item_seq_id,
	p.PRODUCT_ID,
	p.PRODUCT_NAME,
	p.PRODUCT_TYPE_ID,
	p.BRAND_NAME,
	oi.STATUS_ID,
	os.STATUS_DATETIME,
	(SELECT pt.is_physical
    FROM product_type pt
    WHERE pt.product_type_id = p.PRODUCT_TYPE_ID) AS is_physical
FROM
	order_item oi
JOIN order_status os ON
	oi.ORDER_ID = os.ORDER_ID
	AND oi.ORDER_ITEM_SEQ_ID = os.ORDER_ITEM_SEQ_ID
	AND oi.STATUS_ID = 'ITEM_CREATED'
	AND oi.STATUS_ID = os.STATUS_ID
JOIN product p ON
	oi.product_id = p.PRODUCT_ID
WHERE
	(SELECT pt.is_physical
    FROM product_type pt
    WHERE pt.product_type_id = p.PRODUCT_TYPE_ID) = 'y'
AND EXTRACT(year FROM os.STATUS_DATETIME) = 2023
AND EXTRACT(month FROM os.STATUS_DATETIME) = 9;
```
