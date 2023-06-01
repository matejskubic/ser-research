# Target data entity: `data/FixedAssetsV2`

#_API Methods_

## **searchAssets**
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

# **getAsset**
Returns details about an asset number.
## Inbound data
_The data is sent as a JSON object with the following mapping:_
| Source | Destination | Comment |
|--|--|--|
| Id | LegalEntityId |

## Outbound data
_The response as a single JSON object with the following format:_
| Source | Destination | Comment |
|--|--|--|
| FixedAssetNumber | Id| |
| Name| Description | |
| FixedAssetGroupId | Category | |

