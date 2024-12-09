Fetch the order id and contact mech id for the shipping address of the orders completed in October of 2023.
```
select
	ORDER_ID,
	CONTACT_MECH_ID,
	os.STATUS_ID ,
	ocm.CONTACT_MECH_PURPOSE_TYPE_ID
from
	order_contact_mech ocm
join order_status os
		using(order_id)
where
	CONTACT_MECH_PURPOSE_TYPE_ID = 'shipping_location'
	and extract(year from os.STATUS_DATETIME) = "2023"
	and extract(month from os.STATUS_DATETIME) = "10"
	and status_id = 'order_completed';
```
