#_API Methods_

##`POST`**/getPurchaseOrderData**
Returns information about the purchase order with the specified order number.

## Target data entities: `data/PurchaseOrderConfirmationHeaders`, `data/ProductReceiptHeaders`

## Inbound data

_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. If it's not set, 100 records are retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Data entity | Comment |
|--|--|--|--|
| Id | PurchaseOrderNumber | ProductReceiptHeaders | |
| CompanyCode | dataAreaId | ProductReceiptHeaders, PurchaseOrderConfirmationHeaders | |
| Type | PurchaseOrderStatus | PurchaseOrderConfirmationHeaders | Certain item types are to be determined via the type. Possible values are NONE, OPEN, POSTED, and RETURNED. |
| Date | | | Corresponds to the posting date (ISO 8601 format) if the line items are to be determined retrospectively. <div style="color:red">Not implemented.</div>|


## Outbound data (getPurchaseOrderDataResponse)

_The response is a single JSON object with the following format:_

| Source | Destination | Data entity | Comment |
|--|--|--|--|
| PurchaseOrderNumber | Id | ProductReceiptHeaders | Purchase order number, as stored in the ERP system |
| | DocumentType | | Type of the purchase order. Always has a value "STANDARD". |
| `PurchaseOrderStatus` | GRExpected | PurchaseOrderConfirmationHeaders | Boolean value showing whether the line item is still awaiting delivery of goods. If PurchaseOrderStatus value from the data entity has the value "Received", or if the "Type" parameter from the request has the value "NONE", the output value in this field will be False. Otherwise, it will be Trus. |
| | InformativePositions | | An array of line item data (min. 0 objects). The data is intended for informational purposes only; it cannot be used for posting. The list of elements of each item in this array is shown in the table below. (*) |
| OrderVendorAccountNumber | VendorId | PurchaseOrderConfirmationHeaders | |
| | TermsOfPayment | | JSON object whose structure is shown in the table below. (**) |

(*) <b>InformativePositions item structure</b>
As mentioned above, the InformativePositions element of the output object is an array of object with the following structure:
| Source | Destination | Data entity | Comment |
|--|--|--|--|