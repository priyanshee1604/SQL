Fetch the following columns for completed order items for sales orders of SM_STORE product store and that are physical items.
ORDER_ID
ORDER_ITEM_SEQ_ID
PRODUCT_ID
PRODUCT_TYPE_ID
IS_PHYSICAL
IS_DIGITAL
SALES_CHANNEL_ENUM_ID
ORDER_DATE
ENTRY_DATE
STATUS_ID
STATUS_DATETIME
ORDER_TYPE_ID
PRODUCT_ST

```
select
	oi.ORDER_ID,
	oi.STATUS_ID,
	oi.ORDER_ITEM_SEQ_ID,
	oi.PRODUCT_ID,
	p.PRODUCT_TYPE_ID,
	pt.IS_PHYSICAL,
	pt.IS_DIGITAL,
	oh.SALES_CHANNEL_ENUM_ID,
	oh.ORDER_DATE,
	oh.ENTRY_DATE,
	oi.STATUS_ID,
	os.STATUS_DATETIME,
	oh.ORDER_TYPE_ID,
	oh.PRODUCT_STORE_ID
from
	order_item oi
join order_header oh
		on
	oi.order_id = oh.ORDER_ID
join product p
		on
	p.product_id = oi.PRODUCT_ID
join product_type pt
		on
	p.product_type_id = pt.product_type_id
join order_status os
		on
	oi.order_id = os.ORDER_ID
	and oi.ORDER_ITEM_SEQ_ID = os.ORDER_ITEM_SEQ_ID
	and oi.STATUS_ID = os.STATUS_ID
	and oi.STATUS_ID = 'ITEM_COMPLETED'
where
	oh.ORDER_TYPE_ID = 'sales_order'
	and oh.PRODUCT_STORE_ID = "SM_store"
	and pt.is_physical = 'y';
```
