#_API Methods_

##`POST`**/getTaxCode**
Returns all assets for the specified company code and the current date.

# Target data entities: `data/VendorsV3`, `data/TaxGroupDatas`, `TaxCodeValuesV2`

## Inbound data

_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. If it's not set, 100 records are retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Data entity | Comment |
|--|--|--|--|
| CompanyCode | dataAreaId | VendorsV3<br />TaxGroupDatas<br />TaxCodeValuesV2 | Mandatory parameter |
| VendorVATNumber | TaxExemptNumber | VendorsV3 | Optional parameter |
| Date | FromDate / ToDate| TaxCodeValuesV2 | Optional parameter. If it's specified, only the records where this parameter value is between the values of FromDate and ToDate fields from the data entity. |
| PositionData | | | Optional parameter. An object array whose elements have the following fields:<br /><table><tr><th>Source field</th><th>Comment</th></tr><tr><td>Id</td><td>Order number, not related to any data in the data entity</td><tr><td>ArticleType</td><td></td>Optional value, not used anywhere<tr><td>MaterialNo</td><td>Optional value, not used anywhere</td><tr><td>TaxRate</td><td>If the tax rate is known and specified in the request, it will be used to filter the tax codes.</td></tr></table> |

## Outbound data (getTaxCodeResponse)
_The response is in the following format:_
- Result - JSON array with the following fields:

| Source | Destination | Data entity | Comment |
|--|--|--|--|
| | Id | | Equal to the ID specified in the query |
| TaxCodeId | Code | TaxCodeValuesV2 | 
| | PossibleCode | TaxCodeValuesV2 | A string array. If no tax code could be determined unambiguously, the most plausible tax code will be passed in the 'Code' parameter, and other possible tax codes will be listed in 'PossibleCode' |
|  | Rate | Tax code rate. Expected format: 0.03 for 3%; 1.00 for 100%. Equal to the TaxRate value specified in the query |


##`POST`**/getTaxRates**
Determination of tax rates for automatic extraction.

# Target data entity: `data/TaxCodeValuesV2`

## Inbound data
_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| CompanyCode | dataAreaId | Mandatory parameter |
| Date | FromDate / ToDate | Optional parameter. If it's specified, only the records where this parameter value is between the values of FromDate and ToDate fields from the data entity. |
| Code | TaxCodeId | Optional parameter. If the tax code is known, it can be used to filter the tax rates. |

## Outbound data (getTaxRatesResponse)
_The response is in the following format:_
- Rates - JSON array containing tax rates for a specified country. Expected format: 0.03 for 3%; 1.00 for 100%. Each element has the following structure:

| Source | Destination | Comment |
|--|--|--|
| Value | | |