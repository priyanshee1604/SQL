In the past month, which store has the highest number of one-day shipped orders?
```
select
	oisg.FACILITY_ID ,
	f.FACILITY_NAME,
	f.FACILITY_TYPE_ID,
	count(oisg.ORDER_ID) as one_day_shipped_orders
from
	order_item_ship_group oisg
join facility f on
	oisg.FACILITY_ID = f.FACILITY_ID
join facility_type ft on
	f.FACILITY_TYPE_ID = ft.FACILITY_TYPE_ID
join order_status os on
	os.ORDER_ID = oisg.ORDER_ID
	and os.STATUS_ID = 'order_completed'
where
	oisg.SHIPMENT_METHOD_TYPE_ID = 'NEXT_DAY'
	and ft.PARENT_TYPE_ID <> 'VIRTUAL_FACILITY'
group by
	oisg.FACILITY_ID
order by
	one_day_shipped_orders desc
limit 1;
```
