# Target data entity: `data/VendInvoiceJournalHeaders`<span style='font-size:small'> or `data/BESer_VendTrans`, depending on the structure of data->Id parameter.</span>

#_API Methods_

##`POST`**/getPostingStatus**
Returns whether the invoice is posted or open.

## Inbound data

_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. If it's not set, 100 records are retrieved. <span style='color:red'>Not needed here as the query retrieves only 1 record.</span>
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| Id | In the case of vendor invoice journal (`data/VendInvoiceJournalHeaders` data entity):<ul><li>dataAreaId</li><li>journalNumber</li><li>journalName</li></ul>In the case of pending vendor invoice (`data/BESer_VendTrans` data entity):<ul><li>dataAreaId</li><li>AccountNum</li><li>Invoice</li></ul>| Mandatory parameter. The parameter is a pipe-delimited array containing the values for identifying the invoice type. In case the parameter value has 2 pipes, it's a vendor invoice journal, and if there are 3 pipes, it a pending vendor invoice. Otherwise, an error message is thrown. The values contained in this parameter are listed in the Destination column. |
| FinancialDimension | FinancialDimension | Optional parameter |
| DimensionValue | DimensionValue | Optional parameter |

## Outbound data (searchCustomResponse)
_The response is just a status code with the possible values:<ul><li>200 (OK) - The invoice is posted</li><li>0 - The invoice is not posted</li><li>500 - The invoice is not found, or some other error occurred.</li></ul>
