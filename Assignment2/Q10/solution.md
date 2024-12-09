Fetch all the order items that are in the created status and the order type should be a sales order
ORDER_ID
PRODUCT_TYPE_ID
ORDER_LINE_ID
EXTERNAL_ID
SALES_CHANNEL
QUANTITY
ITEM_STATUS 
PRODUCT_ID
BILL_CITY
BILL_COUNTRY
BILL_POSTALCODE
BILL_ADDRESS1
BILL_ADDRESS2
SHIP_CITY
SHIP_COUNTRY
SHIP_POSTALCODE
SHIP_ADDRESS1
SHIP_ADDRESS2
```
select
	oi.ORDER_ID,
	oi.ORDER_ITEM_SEQ_ID as ORDER_LINE_ID,
	oi.PRODUCT_ID,
	p.PRODUCT_TYPE_ID,
	oh.EXTERNAL_ID,
	oh.SALES_CHANNEL_ENUM_ID as SALES_CHANNEL,
	oi.QUANTITY,
	oi.status_id as item_status,
	ocm.CONTACT_MECH_ID as cnt_id_bill,
	ocm.CONTACT_MECH_PURPOSE_TYPE_ID,
	pa.CITY as city_bill,
	pa.COUNTRY_GEO_ID as geo_bill,
	pa.POSTAL_CODE as postal_code_bill,
	pa.ADDRESS1 as add1_bill,
	pa.ADDRESS2 as add2_bill,
	ocm2.CONTACT_MECH_ID as cnt_id_ship,
	ocm2.CONTACT_MECH_PURPOSE_TYPE_ID,
	pa2.CITY as city_ship,
	pa2.COUNTRY_GEO_ID as geo_ship,
	pa2.POSTAL_CODE as postal_code_ship,
	pa2.ADDRESS1 as add1_ship,
	pa2.ADDRESS2 as add2_ship
from
	order_item oi
join order_header oh on
	oi.ORDER_ID = oh.ORDER_ID
join product p
		on
	oi.product_id = p.PRODUCT_ID
join order_contact_mech ocm on
	ocm.ORDER_ID = oi.ORDER_ID
	and ocm.CONTACT_MECH_PURPOSE_TYPE_ID = 'BILLING_LOCATION'
join order_contact_mech ocm2 on
	ocm2.ORDER_ID = oi.ORDER_ID
	and ocm2.CONTACT_MECH_PURPOSE_TYPE_ID = 'SHIPPING_LOCATION'
join postal_address pa
		on
	pa.contact_mech_id = ocm.contact_mech_id
join postal_address pa2 on
	pa2.CONTACT_MECH_ID = ocm2.CONTACT_MECH_ID
where
	oi.STATUS_ID = 'ITEM_CREATED'
	and oh.ORDER_TYPE_ID = 'SALES_ORDER';
```
