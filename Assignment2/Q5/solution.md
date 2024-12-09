Fetch the following data for completed order items in July of 2023
ORDER_ID
ORDER_ITEM_SEQ_ID
SHOPIFY_ORDER_ID
SHOPIFY_PRODUCT_ID
```
select
	oi.ORDER_ID,
	oi.ORDER_ITEM_SEQ_ID,
	oi2.ID_VALUE as SHOPIFY_ORDER_ID,
	gi.id_value as SHOPIFY_PRODUCT_ID,
	oi.STATUS_ID,
	extract(year from os.status_datetime) as year,
	extract(month from os.status_datetime) as month
from
	order_item oi
join order_status os on
	oi.ORDER_ID = os.ORDER_ID
	and
	oi.ORDER_ITEM_SEQ_ID = os.ORDER_ITEM_SEQ_ID
join order_identification oi2 on
	oi.order_id = oi2.ORDER_ID
	and ORDER_IDENTIFICATION_TYPE_ID = 'SHOPIFY_ORD_ID'
join good_identification gi on
	gi.product_id = oi.PRODUCT_ID
	and GOOD_IDENTIFICATION_TYPE_ID = 'SHOPIFY_PROD_ID'
where
	extract(year from os.status_datetime) = 2023
	and
	extract(month from os.status_datetime) = 7
	and os.STATUS_ID = 'ITEM_COMPLETED';
```
