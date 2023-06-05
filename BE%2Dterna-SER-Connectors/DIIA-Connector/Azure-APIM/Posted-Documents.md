# Target data entity: `data/BESer_VendInvoiceJours`

#_API Methods_

##`POST`**/searchPosted**
Returns the previously posted invoice or credit memo based on business data.

## Inbound data

_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. If it's not set, 100 records are retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| CompanyCode | dataAreaId | Mandatory parameter |
| OrderType | `PurchId` | Mandatory parameter. If this parameter has a value "WIPO", only the records where PurchId field value is not blank (null or empty string) will be retrieved. If this field value is "WOPO", only the records where PurchId field value is blank will be retrieved. Otherwise, nothing is retrieved.
| Date | InvoiceDate | Optional parameter |
| Number | InvoiceId | Optional parameter |

## Outbound data (searchPostedResponse)
_The response is in the following format:_
- SearchResult - JSON array with the following fields:

| Source | Destination | Comment |
|--|--|--|
| dataAreaId | CompanyCode |
| InvoiceDate | Date | Displayed in the format "yyyy-MM-dd". | 
| LedgerVoucher | Id | |
| `PurchId` | OrderType | If PurchId field value is blank (null or empty string), the destination value will be "WOPO". If it is empty, the destination value is "WIPO". |
- Truncated (true or false, depending on whether all the data is displayed or not)

##`POST`**/getCaptureState**
Returns the acquisition status of the invoice in the ERP system.
## Inbound data
_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. Unnecessary here, as only one record is eventually retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| Id | <ul><li>dataAreaId</li><li>InvoiceAccount</li><li>InvoiceId</li><li>InvoiceDate</li></ul> | Mandatory parameter. This has to be a pipe-delimited string that converts to an array with the elements listed in the Destination column. All the elements of the array are used for filtering, with the logical AND between them. If the parameter value is not properly supplied, no data will be retrived. |
| Description | Name | Optional parameter |

## Outbound data (getAssetResponse)
_The response is a single JSON object with the following format:_
| Source | Destination | Comment |
|--|--|--|
| FixedAssetNumber | Id| |
| Name| Description | |
| FixedAssetGroupId | Category | |

