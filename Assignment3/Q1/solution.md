How many single-item orders were fulfilled from warehouses in the last month?
```
select
	oi.ORDER_ID,
	count(oi.oRDER_ITEM_SEQ_ID) as cnt,
	oi.oRDER_ITEM_SEQ_ID,
	f.FACILITY_TYPE_ID,
	oi.STATUS_ID,
	os.STATUS_DATETIME
from
	order_item oi
join order_item_ship_group oisg on
	oisg.ORDER_ID = oi.ORDER_ID
	and oi.SHIP_GROUP_SEQ_ID = oisg.SHIP_GROUP_SEQ_ID
join facility f on
	oisg.FACILITY_ID = f.FACILITY_ID
join facility_type ft on
	f.FACILITY_TYPE_ID = ft.FACILITY_TYPE_ID
join order_status os on
	oi.ORDER_ID = os.ORDER_ID
	and oi.ORDER_ITEM_SEQ_ID = os.ORDER_ITEM_SEQ_ID
	and os.STATUS_ID = oi.STATUS_ID
where
	ft.PARENT_TYPE_ID = "DISTRIBUTION_CENTER"
	and oi.STATUS_ID = "item_completed"
	and os.STATUS_DATETIME >= curdate() - interval 1 month
group by
	oi.ORDER_ID
having
	count(oi.oRDER_ITEM_SEQ_ID) = 1;
```
