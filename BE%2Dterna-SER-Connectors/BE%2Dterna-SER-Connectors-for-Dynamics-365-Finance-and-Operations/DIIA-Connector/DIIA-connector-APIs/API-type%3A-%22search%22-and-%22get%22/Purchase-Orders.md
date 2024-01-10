## D365FO Target data entities: `data/PurchaseOrderConfirmationHeaders with PurchaseOrderConfirmationLines`, `data/ProductReceiptHeaders with ProductReceiptLines`, `data/TaxGroupDatas`, `data/TaxItemGroups`, `data/TaxCodeValuesV2`

#_API Methods_

##`POST`**/getPurchaseOrderData**
Returns information about the purchase order with the specified order number.

## Inbound data

_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. If it's not set, 100 records are retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Data entity | Comment |
|--|--|--|--|
| Id | PurchaseOrderNumber | ProductReceiptHeaders | |
| CompanyCode | dataAreaId | ProductReceiptHeaders, PurchaseOrderConfirmationHeaders | |
| Type | PurchaseOrderStatus | PurchaseOrderConfirmationHeaders | Certain item types are to be determined via the type. Possible values are NONE, OPEN, POSTED, and RETURNED. |
| Date | | | Corresponds to the posting date (ISO 8601 format) if the line items are to be determined retrospectively. Note: Not implemented by design.|


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
| `PurchaseOrderNumber-LineNumber` | Id | PurchaseOrderConfirmationLines | Purchase order number with purchase order line number and a dash between them. |
| `ProductType_BESer` | ArticleType | PurchaseOrderConfirmationLines | Possible values are GOOD or SERVICE, depending on the value in the field ProductType_BESer. |
| CurrencyCode | Currency | PurchaseOrderConfirmationHeaders | Line item currency. |
| LineDescription | Description | PurchaseOrderConfirmationLines | The description of the goods, services, or incidental costs. |
| | GRType | PurchaseOrderConfirmationLines | Defines what type of item it is in relation to the goods receipt. The following values ​​are supported and affect the GR parameters: NONE, GREXPECTED, GRBIV. Multiple factors affect this output value. |
| PurchasePrice | NetUnit | PurchaseOrderConfirmationLines | The net unit price of the purchase order line item |
| OrderedPurchaseQuantity - ReceivedPurchaseQuantity | Quantity | PurchaseOrderConfirmationLines | Difference between ordered and received order line quantity. |
| PurchaseUnitSymbol | Unit | PurchaseOrderConfirmationLines | The unit of purchase order line item |
| | Variances | | JSON object containing the tolerable quantity and price variance for a line item. The object's structure is shown in the table below. (***) |
| ItemNumber or ProcurementProductCategoryName| ArticleNoCustomer | PurchaseOrderConfirmationLines| Customer's article number |
| ExternalItemNumber | ArticleNoVendor | PurchaseOrderConfirmationLines | Vendor's article number |
| | RAType | | Defines whether the item requires review and approval. Possible values: DONE, REQUIRED. Note: Not implemented by design. |
| | TaxCode | TaxGroupDatas | The tax code of purchase order line item |
| | TaxRate | TaxCodeValuesV2 | The tax rate of purchase order line item. Expected format: 0.03 for 3%; 1.00 for 100% |
| | AlternativePackagings | | List of alternative package sizes (min. 1 object). Note: Not implemented by design. |
| ProductReceiptDate | GRDate | ProductReceiptHeaders | Corresponds to the goods receipt date (ISO 8601 format), as it is stored in the ERP system. |
| ProductReceiptNumber | GRDeliveryNoteNumber | ProductReceiptLines | The list of delivery numbers from the delivery note. |
| RecordId | GRId | ProductReceiptLines | The goods receipt number that corresponds to the ID in the ERP system. |
| | GRPosition | | The line item ID from the goods receipt. Note: Not implemented by design. |

(**) <b>TermsOfPayment object structure</b>
| Source | Destination | Data entity | Comment |
|--|--|--|--|
| | Discounts | | JSON array containing discount details, sorted ascending by 'Days'. Note: Not implemented by design. |
| FixedDueDate - AccountingDate | DueDays | PurchaseOrderConfirmationHeaders | Number of days until payment is due.  |
| | Id | | Terms of payment key. Note: Not implemented by design. |
| AccountingDate | BaseLineDate | PurchaseOrderConfirmationHeaders | Baseline date in terms of payment (in ISO 8601 format) |
| VendorPaymentMethodName | PaymentMethod | PurchaseOrderConfirmationHeaders | |

(***) <b>Variances object structure</b>
| Source | Destination | Data entity | Comment |
|--|--|--|--|
| PurchasePrice | ExpectedPrice | | The outstanding balance for the line item |
| OrderedPurchaseQuantity | ExpectedQuantity | PurchaseOrderConfirmationLines | The remaining quantity for the line item |
| | PriceDownward | | The lower price limit for the line item. (****) |
| | PriceUpward | | The upper price limit for the line item. (****) |
| | QuantityDownward | | The lower quantity limit for the line item. (****) |
| | QuantityUpward | | | The upper quantity limit for the line item. (****) |

 (****) All the Downward/Upward values from the Variances object are JSON objects with the following fields:
| Source | Destination | Data entity | Comment |
|--|--|--|--|
| | Type | | Type of the variance. Possible values: NONE, RELATIVE, ABSOLUTE, UNLIMITED. For the Downward items, the output value is always "UNLIMITED", and for the Uprard values, it is always "NONE". |
| | Value | | The value of the variance for type 'RELATIVE' or 'ABSOLUTE'. The value of the variance that is still possible is returned for type 'ABSOLUTE'. The expected format for type 'RELATIVE': 0.03 for 3%; 1.00 for 100%. Note: Not implemented by design. |