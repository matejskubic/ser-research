# Target data entity: `data/FixedAssetsV2`

#_API Methods_

## **searchAssets**
Returns all assets for the specified company code and the current date.

## Inbound data

_The data is sent as a JSON object with the following mapping: _
| Source | Destination | Comment |
|--|--|--|
| Id | FixedAssetNumber | 
| Description | Name |
| Category | FixedAssetGroupId |

## Outbound data (searchAssetsResponse)
_The response arrives in the following format:_
- SearchResult - JSON array with the following fields:

| Source | Destination | Comment |
|--|--|--|
| FixedAssetNumber | Id| |
| dataAreaId | CompanyCode |
| | Date | If the Date value is passed in the parameters, that value is shown; otherwise, the current date is shown. The value is displayed in the format "yyyy-MM-dd"<br />Note: this Date parameter is not actually implemented in the search criteria. | 
| Name| Description | |
| FixedAssetGroupId | Category | |

- Truncated (true or false, depending on whether all the data is displayed or not)


# **getRecipientMasterData**
Returns detailed information about a single Invoice Recipient.
## Inbound data
_The data is sent as a JSON object with the following mapping:_
| Source | Destination | Comment |
|--|--|--|
| Id | LegalEntityId |

## Outbound data
_The response as a single JSON object with the following format:_
| Source | Destination | Comment |
|--|--|--|
| LegalEntityId| Id| Lowercase |
| Name | Name |
| PrimaryContactEmail| Email |
| PrimaryContactURL | URL |               |
| VATNum | VATNumber | |
| StartDateOfBusiness | Date| in the format "yyyy-MM-dd" |
| AddressStreet | Street | New line in the source data is replaced by a space character |
| AddressCity | City |
| AddressZipCode | ZIP |
| AddressCountryRegionISOCode | Country |
| LegalEntityId | CompanyCode | Lowercase |
| Name2 | null |
| POBox | null |
| POZIP | null |
| TAXNumber | null |
| VATNumbers | null |
| Auxiliaries |  | JSON object consisting of: <br /> <ul><li>CompanyForm, consisting of:</li><ul><li>Form (empty JSON array)</li><li>Name (empty JSON array)</li></ul><li>MatchCodes, consisting of</li><ul><li>Negatives (empty JSON array)</li><li>Positives (empty JSON array)</li></ul><li>Vendors (empty JSON array)</li></ul>


