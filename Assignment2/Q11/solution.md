Fetch all the customers created in June 2023.
```
select
	p.PARTY_ID ,
	p.PARTY_TYPE_ID,
	p.STATUS_ID,
	p.created_date,
	pr.role_type_id
from
	party p
join party_role pr on
	p.PARTY_ID = pr.PARTY_ID
	and pr.ROLE_TYPE_ID = "customer"
where CREATED_DATE between "2023-06-01" and "2023-06-30";
```
