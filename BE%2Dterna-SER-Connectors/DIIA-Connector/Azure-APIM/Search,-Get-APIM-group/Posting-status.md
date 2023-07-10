# Target data entity: `data/VendInvoiceJournalHeaders`<span style='font-size:small'> or `data/BESer_VendTrans`, depending on the structure of data->Id parameter.</span>

#_API Methods_

##`POST`**/getPostingStatus**
Returns whether the invoice is posted or open.

## Inbound data

_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. If it's not set, 100 records are retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| Id | dataAreaId | Mandatory parameter |
| FinancialDimension | FinancialDimension | Optional parameter |
| DimensionValue | DimensionValue | Optional parameter |

## Outbound data (searchCustomResponse)
_The response is a JSON array with the following fields:

| Source | Destination | Comment |
|--|--|--|
| DimensionValue | DimensionValue | |
| Description | Description |
| CompanyCode | CompanyCode | | 
| GroupDimension | GroupDimension | |
| IsSuspended | IsSuspended | |
| IsBlockedForManualEntry | IsBlockedForManualEntry | |
| IsTotal | IsTotal | |
- Truncated (true or false, depending on whether all the data is displayed or not)