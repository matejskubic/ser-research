# Target data entity: `data/PurchaseOrderHeadersV2`

#_API Methods_

##`POST`**/getVendorPurchaseOrders**
Returns all assets for the specified company code and the current date.

## Inbound data

_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. If it's not set, 10 records are retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| CompanyCode | dataAreaId | Mandatory parameter |
| VendorId | InvoiceVendorAccountNumber | Mandatory parameter |
| Date | | Optional parameter. <div style="color: red">Not implemented. </div> |

## Outbound data (getVendorPurchaseOrdersResponse)
_The response is in the following format:_
- Result - JSON array with the following fields:

| Source | Destination | Comment |
|--|--|--|
| PurchaseOrderNumber | Id| |
| RequestedDeliveryDate | Date |
| PurchaseOrderName | Description | In the format "yyyy-MM-dd" |