Get all the appeasements in July month.
How do we differentiate between returns and appeasements?
Get all the below fields 
RETURN_ID
ENTRY_DATE 
RETURN_ADJUSTMENT_TYPE_ID
AMOUNT
COMMENTS 
ORDER_ID
ORDER_DATE 
RETURN_DATE
PRODUCT_STORE_ID

– Appeasements are made for the shipping refund as well, appeasements are made at the order level and not at the item level, return (appeasements) can have more than one status like created, completed and received.
```
select
	ra.RETURN_ID,
	ra.AMOUNT,
	ra.ORDER_ID,
	rs.STATUS_ID,
	oh.PRODUCT_STORE_ID,
	rs.STATUS_DATETIME,
	rh.ENTRY_DATE,
	rh.RETURN_DATE,
	oh.ORDER_DATE,
	ra.RETURN_ADJUSTMENT_TYPE_ID,
	ra.COMMENTS
from
	return_adjustment ra
join return_status rs on
	rs.RETURN_ID = ra.RETURN_ID
and rs.RETURN_ITEM_SEQ_ID is null
join return_header rh on
	ra.RETURN_ID = rh.RETURN_ID
join order_header oh on
oh.ORDER_ID = ra.ORDER_ID
where
	ra.return_adjustment_type_id = "APPEASEMENT"
and extract(month from rs.status_datetime) = "07";
```
