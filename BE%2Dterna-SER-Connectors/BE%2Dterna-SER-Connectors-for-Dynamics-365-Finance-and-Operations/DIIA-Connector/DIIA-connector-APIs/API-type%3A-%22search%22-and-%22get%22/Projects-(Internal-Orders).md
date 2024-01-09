# D365FO Target data entity: `data/Projects`

#_API Methods_

##`POST`**/searchInternalOrders**
Returns all open internal orders for the specified company code and the current date.

## Inbound data

_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. If it's not set, 100 records are retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| CompanyCode | dataAreaId | Mandatory parameter |
| Id | ProjectID | Optional parameter |
| Date | ActualStartDate | Optional parameter. If it's specified, only the projects whose ActualStartDate is equal to the passed Date parameter will be retrieved |
| Description | ProjectName | Optional parameter |

## Outbound data (searchInternalOrdersResponse)
_The response is in the following format:_
- SearchResult - JSON array with the following fields:

| Source | Destination | Comment |
|--|--|--|
| ProjectID | Id| |
| dataAreaId | CompanyCode |
| ActualStartDate | Date | Displayed in the format "yyyy-MM-dd" | 
| ProjectName | Description | |
- Truncated (true or false, depending on whether all the data is displayed or not)

##`post`**/getInternalOrder**
Returns details of the first asset that satisfies the filtering criteria.
## Inbound data
_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. Unnecessary here, as only one record is eventually retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| CompanyCode | dataAreaId | Mandatory parameter |
| Id | ProjectID | Mandatory parameter |
| Date | ActualStartDate | Optional parameter |

## Outbound data (getInternalOrderResponse)
_The response is a single JSON object with the following format:_
| Source | Destination | Comment |
|--|--|--|
| ProjectID | Id| |
| ProjectName | Description | |

