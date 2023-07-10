# Target data entity: `data/FinancialDimensionValues`

#_API Methods_

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

##`POST`**/getAsset**
Returns details of the first asset that satisfies the filtering criteria.
## Inbound data
_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. Unnecessary here, as only one record is eventually retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| CompanyCode | dataAreaId | Mandatory parameter |
| Id | LegalEntityId | Optional parameter |
| Description | Name | Optional parameter |

## Outbound data (getAssetResponse)
_The response is a single JSON object with the following format:_
| Source | Destination | Comment |
|--|--|--|
| FixedAssetNumber | Id| |
| Name| Description | |
| FixedAssetGroupId | Category | |

