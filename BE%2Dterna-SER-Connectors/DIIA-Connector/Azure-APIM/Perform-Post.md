# Target data entities: `data/TaxGroupDatas`, `data/TaxItemGroups`

#_API Methods_

##`POST`**/performPost**
Post an invoice or credit memo.

## Inbound data

_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. If it's not set, 100 records are retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Data entity | Comment |
|--|--|--|--|
| CompanyCode | dataAreaId | | Mandatory parameter |
|  | Data | | Optional parameter. JSON object with the structure described in the table below. (*) |

(*) <b>Data object structure</b>
| Source | Destination | Data entity | Comment |
|--|--|--|--|
| | Amount | | JSON object with the structure described in the table below. (**)  |
| | Date | | |
| | OrderType | | |
| | Positions | | JSON array with the elements whose structure described in the table below. (***) |
| | RecipientId| | |
| | Type | | |
| | VendorId | | |
| | BankId | | |
| | ERP | | |
| | Number | | |
| | RecipientTransferTo | | |
| | RecipientVATNumber | | |
| | | | |
| | | | |
| | | | |
| | | | |
| | | | |
| | | | |
| | | | |
| | | | |

## Outbound data (performPostResponse)
_The response is in the following format:_
- SearchResult - JSON array with the following fields:

| Source | Destination | Comment |
|--|--|--|
| | Id| |
| dataAreaId | CompanyCode |
| | Number | | 
| | FiscalYear | |
| | Period | |
