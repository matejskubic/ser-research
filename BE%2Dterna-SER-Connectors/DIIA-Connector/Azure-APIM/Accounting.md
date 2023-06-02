TBD
<!--
# Target data entity: 

#_API Methods_

## **checkAccounting**
Returns all assets for the specified company code and the current date.

## Inbound data

_The data is sent as a JSON object with the following mapping: _
| Source | Destination | Comment |
|--|--|--|
| Id | FixedAssetNumber |

## Outbound data (searchAssetsResponse)
_The response arrives in the following format:_
- SearchResult - JSON array with the following fields:

| Source | Destination | Comment |
|--|--|--|
| FixedAssetNumber | Id| |
| dataAreaId | CompanyCode |
| | Date | If the Date value is passed in the parameters, that value is shown; otherwise, the current date is shown. The value is displayed in the format "yyyy-MM-dd"<br />Note: this Date parameter is not actually implemented in the filtering. | 
| Name| Description | |
| FixedAssetGroupId | Category | |
- Truncated (true or false, depending on whether all the data is displayed or not)
-->
