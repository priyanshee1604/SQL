What is the total number of orders originating from New York?
```
select
	count(distinct ORDER_ID)
from
	order_contact_mech ocm
join postal_address pa on
	pa.CONTACT_MECH_ID = ocm.CONTACT_MECH_ID
where
	ocm.CONTACT_MECH_PURPOSE_TYPE_ID = "SHIPPING_LOCATION"
	and city = "New York";
```
