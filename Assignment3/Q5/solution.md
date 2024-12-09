In New York, which product has the highest sales?
```
select
	oi.PRODUCT_ID,
	sum(oi.QUANTITY) as total_Sales,
	sum(oi.QUANTITY * oi.UNIT_PRICE) as grand_total,
	oh.ORDER_TYPE_ID,
	pa.city
from
	order_header oh
join order_item oi on
	oh.ORDER_ID = oi.ORDER_ID
	and oh.ORDER_TYPE_ID = "SALES_ORDER"
	and oi.STATUS_ID = "ITEM_COMPLETED"
join order_item_ship_group oisg on
	oisg.order_id = oi.order_id
	and oi.SHIP_GROUP_SEQ_ID = oisg.SHIP_GROUP_SEQ_ID
join facility f
		on
	f.facility_id = oisg.FACILITY_ID
join facility_contact_mech_purpose fcmp
		on
	f.facility_id = fcmp.FACILITY_ID
	and fcmp.CONTACT_MECH_PURPOSE_TYPE_ID = "PRIMARY_LOCATION"
join postal_address pa on
	pa.CONTACT_MECH_ID = fcmp.CONTACT_MECH_ID
where
	pa.city = "new york"
group by
	oi.PRODUCT_ID
order by
	total_Sales desc
limit 1;
```
