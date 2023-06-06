# Target data entities: `data/VendorsV3`, `data/PaymentTerms`

#_API Methods_

##`POST`**/getTermsOfPayment**
Returns terms of payment for the specified key or vendor. Either 'VendorId' or 'Id' must be specified in the query.
## Inbound data
_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. Unnecessary here, as only one record is eventually retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| CompanyCode | dataAreaId | Mandatory parameter |
| Id | | Optional parameter. Terms of payment key. Must not be set if 'VendorId' is set. |
| Date | | Optional parameter |
| VendorId | VendorAccountNumber | Optional parameter. Terms of payment key. Must not be set if 'Id' is set. |

## Outbound data (getTermsOfPaymentResponse)
_The response is a single JSON object with the following format:_
| Source | Destination | Comment |
|--|--|--|
|  | Id| |
| Name| Description | |
|  |  | |