# Target data entities: `data/VendorsV3`, `data/TaxGroupDatas`, `TaxCodeValuesV2`

#_API Methods_

##`POST`**/getTaxCode**
Returns all assets for the specified company code and the current date.

## Inbound data

_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. If it's not set, 100 records are retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Data entity | Comment |
|--|--|--|--|
| CompanyCode | dataAreaId | VendorsV3<br />TaxGroupDatas<br />TaxCodeValuesV2 | Mandatory parameter |
| VendorVATNumber | TaxExemptNumber | VendorsV3 | Optional parameter |
| Date | FromDate / ToDate| TaxCodeValuesV2 | Optional parameter. If it's specified, only the records where this parameter value is between the values of FromDate and ToDate fields from the data entity. |
| PositionData | | | Optional parameter. An object array whose elements have the following fields:<br /><table><tr><th>Source field</th><th>Comment</th></tr><tr><td>Id</td><td></td><tr><td>ArticleType</td><td></td><tr><td>MaterialNo</td><td></td><tr><td>TaxRate</td><td></td></tr></table> |

## Outbound data (searchAssetsResponse)
_The response is in the following format:_
- Result - JSON array with the following fields:

| Source | Destination | Data entity | Comment |
|--|--|--|--|
| Id | Id | | |
| dataAreaId | CompanyCode |
| | Date | If the Date value is passed in the parameters, that value is shown; otherwise, the current date is shown. The value is displayed in the format "yyyy-MM-dd"<br />Note: this Date parameter is not actually implemented in the filtering. | 
| Name| Description | |
| FixedAssetGroupId | Category | |
- Truncated (true or false, depending on whether all the data is displayed or not)

<!--
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
-->