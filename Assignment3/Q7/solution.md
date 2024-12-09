On a city-wise basis, what is the analysis of returns?
```
select
	city,
	count(rh.RETURN_ID)
from
	return_header rh
join return_contact_mech rcm on
	rh.RETURN_ID = rcm.RETURN_ID
	and rcm.CONTACT_MECH_PURPOSE_TYPE_ID = "SHIPPING_LOCATION"
join postal_address pa on
	pa.CONTACT_MECH_ID = rcm.CONTACT_MECH_ID
group by
	pa.CITY;
```
