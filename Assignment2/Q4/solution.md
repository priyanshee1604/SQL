Fetch the following columns for created orders. These should be sales orders.
ORDER_ID
TOTAL_AMOUNT
PAYMENT_METHOD
SHOPIFY_ORDER_NAME
NOTE: 
The total amount represents the total amount of the order.
The payment method is the method by which payment was made, like Cash, mastercard, visa, paypal, etc.
```
select
	oh.ORDER_ID,
	oh.grand_total as TOTAL_AMOUNT,
	opp.PAYMENT_METHOD_TYPE_ID,
	oi.ID_VALUE as SHOPIFY_ORDER_NAME
from
	order_header oh
join order_identification oi
	on
	oi.ORDER_ID = oh.ORDER_ID
	and oi.ORDER_IDENTIFICATION_TYPE_ID = "SHOPIFY_ORD_NAME"
join order_payment_preference opp
		on
	oh.order_id = opp.ORDER_ID
where
	oh.status_id = 'order_created'
	and oh.order_type_id = 'sales_order';
```
