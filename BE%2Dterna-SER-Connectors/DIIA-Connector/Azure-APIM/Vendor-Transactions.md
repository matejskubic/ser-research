#_API Methods_

##`POST`**/getPurchaseOrderData**
Returns the payment status of the invoice in the ERP system.

## Target data entity: `data/PurchaseOrderConfirmationHeaders`

## Inbound data

_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. If it's not set, 100 records are retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| Id | | |
| CompanyCode | dataAreaId | |
| Date | | |


## Outbound data (getPaymentStateResponse)
**TBD**
<!--
_The response is a single JSON object with the following format:_

| Source | Destination | Comment |
|--|--|--|
| `Closed` | Status | If there's any record in the response where the column named <b>Closed</b> (this column contains the date data type) has a value other than F&O's null date (01/01/1900 12:00:00), the value in this output column will be "_PAID_". Otherwise, the value in this column will be "_OPEN_". |
| `Closed` | Date | If the value in the previous field is "_PAID_", the value in this field will be the value from the <b>Closed</b> field from the given record. Otherwise, it will be the current date. Either way, this value is displayed in the format "yyyy-MM-dd". |

-->

##`POST`**/getVendorPurchaseOrders**
Returns open purchase orders of a specific vendor.

## Target data entity: `data/PurchaseOrderHeadersV2`

## Inbound data
_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. Unnecessary here, as only one record is eventually retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| CompanyCode | dataAreaId | Mandatory parameter |
| VendorId | InvoiceVendorAccountNumber | Mandatory parameter |


## Outbound data (getVendorPurchaseOrdersResponse)
_The response is a single JSON object with the following format:_
| Source | Destination | Comment |
|--|--|--|
| PurchaseOrderNumber  | Id| |
| RequestedDeliveryDate | Date | In the format "yyyy-MM-dd" |
| Description | PurchaseOrderName |