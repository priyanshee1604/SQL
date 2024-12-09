Fetch the inventory variances of the products where the reason is ‘VAR_LOST’ or VAR_DAMAGED.
```
select
	ii.INVENTORY_ITEM_ID,
	iiv.PHYSICAL_INVENTORY_ID,
	PRODUCT_ID,
	INVENTORY_ITEM_TYPE_ID ,
	FACILITY_ID,
	iiv.VARIANCE_REASON_ID
from
	inventory_item_variance iiv
join inventory_item ii
		on
	iiv.inventory_item_id = ii.INVENTORY_ITEM_ID
	and iiv.VARIANCE_REASON_ID in ('VAR_LOST', 'VAR_DAMAGED');
```
