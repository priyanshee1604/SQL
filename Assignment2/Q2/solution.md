Fetch the following columns for completed return items of SM_STORE for ecom return channel.
RETURN_ID 
ORDER_ID
PRODUCT_STORE_ID 
STATUS_DATETIME
ORDER_NAME 
FROM_PARTY_ID 
RETURN_DATE 
ENTRY_DATE
RETURN_CHANNEL_ENUM_ID

```
SELECT
   ri.RETURN_ID,
   ri.RETURN_ITEM_SEQ_ID,
   ri.ORDER_ID,
   oh.PRODUCT_STORE_ID,
   oh.ORDER_NAME,
   rh.FROM_PARTY_ID,
   rh.RETURN_DATE,
   rh.ENTRY_DATE,
   rh.RETURN_CHANNEL_ENUM_ID,
   rs.STATUS_DATETIME
FROM
   return_item ri
JOIN
   order_item oi ON ri.ORDER_ID = oi.ORDER_ID
   AND ri.ORDER_ITEM_SEQ_ID = oi.ORDER_ITEM_SEQ_ID
   AND ri.STATUS_ID = 'return_completed'
JOIN
   order_header oh ON oh.ORDER_ID = oi.ORDER_ID
JOIN
   return_header rh ON rh.return_id = ri.RETURN_ID
JOIN
   return_status rs ON rs.RETURN_ID = ri.RETURN_ID
   AND rs.RETURN_ITEM_SEQ_ID = ri.RETURN_ITEM_SEQ_ID
   AND rs.STATUS_ID = ri.STATUS_ID
WHERE
   oh.PRODUCT_STORE_ID = 'sm_store'
   AND rh.RETURN_CHANNEL_ENUM_ID = 'ECOM_RTN_CHANNEL';
```
