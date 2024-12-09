Fetch the following details for orders completed in August of 2023.
PRODUCT_ID
PRODUCT_TYPE_ID
PRODUCT_STORE_ID 
TOTAL_QUANTITY
INTERNAL_NAME 
FACILITY_ID
EXTERNAL_ID 
FACILITY_TYPE_ID 
ORDER_HISTORY_ID 
ORDER_ID
ORDER_ITEM_SEQ_ID
SHIP_GROUP_SEQ_ID

Here there is some discrepancy in the data of order_history entity (we store data at item level in order_history)
The order history entity contains the full order life cycle, but some orders which are completed do not have event_type_enum_id marked as item_shipped or item_cancelled.

Here we have 4 status, for the item to be completed it should either be canceled or be shipped.
Example check the status for the order id 43620 seq 01 the item is completed but in order history it does not have a record marked as item shipped thus some orders are removed from the above answer data set.
```
select
	oh.ORDER_ID,
	oh.STATUS_ID as orders_staus,
	oi.STATUS_ID as orditems_status,
	oi.order_item_seq_id,
	oh.ORDER_NAME,
	p.INTERNAL_NAME,
	oh.EXTERNAL_ID,
	oi.PRODUCT_ID,
	p.PRODUCT_TYPE_ID,
	oh.PRODUCT_STORE_ID,
	oi.quantity as TOTAL_QUANTITY,
	oisg.SHIP_GROUP_SEQ_ID,
	oisg.FACILITY_ID,
	f.FACILITY_TYPE_ID,
	oh2.ORDER_HISTORY_ID,
	oh2.EVENT_TYPE_ENUM_ID
from
	order_header oh
join order_item oi
		on
	oi.order_id = oh.ORDER_ID
join order_status os on
	os.order_id = oh.ORDER_ID
	and oh.STATUS_ID = 'order_completed'
	and os.STATUS_ID = 'order_completed'
join product p
		on
	p.product_id = oi.PRODUCT_ID
join order_item_ship_group oisg
	on
	oi.ORDER_ID = oisg.ORDER_ID
	and oi.SHIP_GROUP_SEQ_ID = oisg.SHIP_GROUP_SEQ_ID
join facility f on
	f.facility_id = oisg.FACILITY_ID
join order_history oh2
		on
	oh.order_id = oh2.ORDER_ID
	and oi.ORDER_ITEM_SEQ_ID = oh2.ORDER_ITEM_SEQ_ID
	and ( oh2.EVENT_TYPE_ENUM_ID = "ITEM_CANCELLED"
		or oh2.EVENT_TYPE_ENUM_ID = "ITEM_SHIPPED")
where
	extract(year from os.STATUS_DATETIME) = '2023'
	and
	extract(month from os.STATUS_DATETIME) = '08';
```
