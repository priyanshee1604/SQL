Leading up to the New Year, what is the count of orders shipped from stores in the 25 days preceding the New Year?
```
select
	count(distinct oi.ORDER_ID)
from
	 order_item oi
join order_item_ship_group oisg on
	oisg.ORDER_ID = oi.ORDER_ID
	and oisg.SHIP_GROUP_SEQ_ID = oi.SHIP_GROUP_SEQ_ID
join facility f
		on
	f.facility_id = oisg.FACILITY_ID
join facility_type ft on
	ft.FACILITY_TYPE_ID = f.FACILITY_TYPE_ID
join order_status os
		on
	os.ORDER_ID = oi.ORDER_ID
	and os.STATUS_ID = 'ORDER_COMPLETED'
where
	ft.PARENT_TYPE_ID = "PHYSICAL_STORE"
	and os.STATUS_DATETIME between "2020-12-07" and "2020-12-31";
```
