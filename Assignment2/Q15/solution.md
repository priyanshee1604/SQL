Find all the orders that have more than one return
```
select
	ORDER_ID,
	count(distinct RETURN_ID) as total_returns
from
	return_item ri
where
	ORDER_ID is not null
group by
	ORDER_ID
having
	total_returns >1;
```
