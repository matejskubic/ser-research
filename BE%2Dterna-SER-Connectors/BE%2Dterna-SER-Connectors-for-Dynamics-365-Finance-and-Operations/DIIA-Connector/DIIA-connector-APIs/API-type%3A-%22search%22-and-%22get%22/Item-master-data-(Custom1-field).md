# D365FO Target data entity: `data/ReleasedProductsV2`, <span style='font-size:smaller'>including `ProductV2` sub-entity.</span>

#_API Methods_

##`POST`**/searchCustom1**
This is an empty function that can be used to implement the logic for custom account assignment field 1.

## Inbound data

_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. If it's not set, 100 records are retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| CompanyCode | dataAreaId | Mandatory parameter |
| Id | ItemNumber | Optional parameter |
| SearchName | SearchName | Optional parameter |

## Outbound data (searchCustom1Response)
_The response is in the following format:_
- SearchResult - JSON array with the following fields:

| Source | Destination | Comment |
|--|--|--|
| ItemNumber | Id| |
| dataAreaId | CompanyCode |
| SearchName | SearchName | | 
| ProductName| Name | |
| ProductDescription | Description | From the ProductV2 data entity |
- Truncated (true or false, depending on whether all the data is displayed or not)

##`POST`**/getCustom1**
This is an empty function that can be used to implement the logic for custom account assignment field 1.

## Inbound data

_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. If it's not set, 100 records are retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| CompanyCode | dataAreaId | Mandatory parameter |
| FinancialDimension | FinancialDimension | Optional parameter |
| DimensionValue | DimensionValue | Optional parameter |

## Outbound data (getCustom1Response)
_The response is a single JSON object with the following format:_

| Source | Destination | Comment |
|--|--|--|
| ItemNumber | Id| |
| dataAreaId | CompanyCode |
| SearchName | SearchName | | 
| ProductName| Name | |
| ProductDescription | Description | |

