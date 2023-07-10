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
| Id | In the case of vendor invoice journal (`data/VendInvoiceJournalHeaders` data entity):<ul><li>dataAreaId</li><li>journalNumber</li><li>journalName</li></ul>In the case of pending vendor invoice (`data/BESer_VendTrans` data entity):<ul><li>dataAreaId</li><li>AccountNum</li><li>Invoice</li></ul>| Mandatory parameter. The parameter is a pipe-delimited array containing the values for identifying the invoice type. In case the parameter value has 2 pipes, it's a vendor invoice journal, and if there are 3 pipes, it a pending vendor invoice. Otherwise, an error message is thrown. The values contained in this parameter are listed in the Destination column. |
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