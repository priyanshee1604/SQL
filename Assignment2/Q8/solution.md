Find all the orders whose two or more items are completed but the orders are still in the approved status.
```
select
	oi.order_id,
	count(oi.ORDER_ITEM_SEQ_ID) as cnt
from
	order_item oi
join order_header oh
		on
	oi.order_id = oh.ORDER_ID
where
	oi.STATUS_ID = 'ITEM_COMPLETED'
	and oh.status_id = 'order_Approved'
group by
	oi.ORDER_ID
having
	cnt>1;
```
