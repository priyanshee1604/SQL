Fetch all the physical items completed from Warehouse in September of 2023.
```
select
	oi.order_id,
	oi.order_item_seq_id,
	oi.STATUS_ID ,
	oisga.SHIP_GROUP_SEQ_ID ,
	os.STATUS_DATETIME,
	f.FACILITY_ID,
	pt.is_physical,
	f.FACILITY_TYPE_ID,
	f.FACILITY_NAME
from
	order_item oi
join order_status os on
	oi.ORDER_ID = os.ORDER_ID
	and oi.ORDER_ITEM_SEQ_ID = os.ORDER_ITEM_SEQ_ID
	and oi.STATUS_ID = 'ITEM_COMPLETED'
	and oi.STATUS_ID = os.STATUS_ID
join product p on
	oi.product_id = p.PRODUCT_ID
join product_type pt on
	pt.product_type_id = p.PRODUCT_TYPE_ID
	and is_physical = 'y'
join order_item_ship_group_assoc oisga on
	oi.ORDER_ID = oisga.ORDER_ID
	and oi.order_item_seq_id = oisga.ORDER_ITEM_SEQ_ID
join order_item_ship_group oisg on
	oisg.ORDER_ID = oisga.ORDER_ID
	and oisg.ship_group_seq_id = oisga.SHIP_GROUP_SEQ_ID
join facility f
		on
	oisg.facility_id = f.FACILITY_ID
join facility_type ft on
	ft.FACILITY_TYPE_ID = f.FACILITY_TYPE_ID
	and ft.PARENT_TYPE_ID = "DISTRIBUTION_CENTER"
where
	extract(year from os.STATUS_DATETIME) = "2023"
	and extract(month from os.STATUS_DATETIME) = '09';
```
