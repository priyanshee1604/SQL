How many orders with a single return were recorded in the last month?
```
select
	count(*) as order_return
from
	(
	select
		count(ORDER_ID) as countt
	from
		return_item ri
	join return_status rs
on
		rs.RETURN_id = ri.RETURN_ID
		and rs.RETURN_ITEM_SEQ_ID = ri.RETURN_ITEM_SEQ_ID
		and rs.STATUS_ID = "RETURN_COMPLETED"
		and rs.STATUS_ID = ri.STATUS_ID
	where
		rs.STATUS_DATETIME >= curdate() - interval 1 month
	group by
		ORDER_ID
	having
		countt = 1) tab;
```
