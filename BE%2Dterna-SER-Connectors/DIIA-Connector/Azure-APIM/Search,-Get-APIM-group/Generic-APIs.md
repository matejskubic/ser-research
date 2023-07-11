# Target data entity: `Any existing data entity. Data entity name is one of the inbound parameters`

#_API Method_

##`GET`**/data/{EntityName}**
Search Custom Generic

## Inbound data

_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. If it's not set, 100 records are retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| EntityName | | Mandatory parameter |
| Id | FixedAssetNumber | Optional parameter |
| Description | Name | Optional parameter |
| Category| FixedAssetGroupId | Optional parameter |

## Outbound data (searchAssetsResponse)
_The response is in the following format:_
- SearchResult - JSON array with the following fields:

| Source | Destination | Comment |
|--|--|--|
| FixedAssetNumber | Id| |
| dataAreaId | CompanyCode |
| | Date | If the Date value is passed in the parameters, that value is shown; otherwise, the current date is shown. The value is displayed in the format "yyyy-MM-dd"<br />Note: this Date parameter is not actually implemented in the filtering. | 
| Name| Description | |
| FixedAssetGroupId | Category | |
- Truncated (true or false, depending on whether all the data is displayed or not)