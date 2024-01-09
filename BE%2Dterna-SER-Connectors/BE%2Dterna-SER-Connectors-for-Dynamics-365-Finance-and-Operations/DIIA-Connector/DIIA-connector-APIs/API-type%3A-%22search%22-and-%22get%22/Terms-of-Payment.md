# D365FO Target data entities: `data/VendorsV3`, `data/PaymentTerms`

#_API Methods_

##`POST`**/getTermsOfPayment**
Returns terms of payment for the specified key or vendor. Either 'VendorId' or 'Id' must be specified in the query.
## Inbound data
_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. Unnecessary here, as only one record is eventually retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Data entity | Comment |
|--|--|--|--|
| CompanyCode | dataAreaId | VendorsV3, PaymentTerms | Mandatory parameter |
| Id | Name | PaymentTerms | Optional parameter. Terms of payment key. Must not be set if 'VendorId' is set. |
| Date | | | <div style="color:red">Not implemented</div> |
| VendorId | VendorAccountNumber | VendorsV3 | Optional parameter. Terms of payment key. Must not be set if 'Id' is set. |

## Outbound data (getTermsOfPaymentResponse)
_The response is a single JSON object with the following format:_
| Source | Destination | Data entity | Comment |
|--|--|--|--|
|  | Discounts | | List of discount details (min. 0 objects), sorted ascending by 'Days', with the following items:<table><tr><th>Name</th><th>Description</th></tr><tr><td>Days</td><td>Days until discount expires</td></tr><tr><td>Discount</td><td>Discount percent. Expected format: 0.03 for 3%</td></tr></table><div style="color:red">Not implemented.</div> |
| NumberOfDays | DueDays | PaymentTerms | Number of days until payment is due |
| | Id | PaymentTerms | Terms of payment key |
| | BaseLineDate  | | Baseline date in terms of payment. <div style="color:red">Not implemented.</div> |
| PaymentMethodType | PaymentMethod | PaymentTerms | | 