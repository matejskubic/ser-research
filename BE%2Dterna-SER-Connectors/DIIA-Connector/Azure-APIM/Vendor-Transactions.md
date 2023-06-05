#_API Methods_

##`POST`**/getPaymentState**
Returns the payment status of the invoice in the ERP system.

## Target data entity: `data/PurchaseOrderHeadersV2`

## Inbound data

_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. If it's not set, 100 records are retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| Id | <ul><li>dataAreaId</li><li>AccountNum</li><li>Invoice</li><li>TransDate</li></ul> | Mandatory parameter. This has to be a pipe-delimited string that converts to an array with the elements listed in the Destination column. All the elements of the array are used for filtering, with the logical AND between them. No data will be retrieved if the parameter value is not properly supplied. |


## Outbound data (getPaymentStateResponse)
_The response is a single JSON object with the following format:_

| Source | Destination | Comment |
|--|--|--|
| `Closed` | Status | If there's any record in the response where the column named <b>Closed</b> (this column contains the date data type) has a value other than F&O's null date (01/01/1900 12:00:00), the value in this output column will be "_PAID_". Otherwise, the value in this column will be "_OPEN_". |
| `Closed` | Date | If the value in the previous field is "_PAID_", the value in this field will be the value from the <b>Closed</b> field from the given record. Otherwise, it will be the current date. Either way, this value is displayed in the format "yyyy-MM-dd". |



##`POST`**/getVendorPurchaseOrders**
Returns details of the first asset that satisfies the filtering criteria.

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