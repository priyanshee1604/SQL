In the period following the New Year, what is the number of orders shipped from stores in the first 25 days?
```
SELECT 
    COUNT(DISTINCT oi.ORDER_ID)
FROM 
    order_item oi
JOIN 
    order_item_ship_group oisg 
    ON 
        oisg.ORDER_ID = oi.ORDER_ID
        AND oisg.SHIP_GROUP_SEQ_ID = oi.SHIP_GROUP_SEQ_ID
JOIN 
    facility f 
    ON 
        f.facility_id = oisg.FACILITY_ID
JOIN 
    facility_type ft 
    ON 
        ft.FACILITY_TYPE_ID = f.FACILITY_TYPE_ID
JOIN 
    order_status os 
    ON 
        os.ORDER_ID = oi.ORDER_ID
        AND os.STATUS_ID = 'ORDER_COMPLETED'
WHERE 
    ft.PARENT_TYPE_ID = 'PHYSICAL_STORE'
    AND os.STATUS_DATETIME BETWEEN '2021-01-01' AND '2021-01-25';
```
