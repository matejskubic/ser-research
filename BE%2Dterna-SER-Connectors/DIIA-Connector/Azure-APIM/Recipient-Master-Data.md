# Target data entity: `data/LegalEntities`

#_API Methods_

## **searchRecipientMasterData**

## Inbound data

_The data is sent as a JSON object with the following mapping:_
| Source | Destination | Comment |
|--|--|--|
| CompanyCode | LegalEntityId | Lowercase | 
| Email | PrimaryContactEmail |
| Name | Name |
| URL | PrimaryContactURL|               |
| VATNumber | VATNum |

## Outbound data
_The response comes in the following format:_
- SearchResult - JSON array with the following fields:

| Source | Destination | Comment |
|--|--|--|
| LegalEntityId| Id| Lowercase |
| Name | Name |
| PrimaryContactURL | URL |               |
| VATNum | VATNumber | |
| StartDateOfBusiness | Date| in the format "yyyy-MM-dd" |
| AddressStreet | Street | New line in the source data is replaced by a space character |
| AddressCity | City |
| AddressZipCode | ZIP |
| AddressCountryRegionISOCode | Country |
| LegalEntityId | CompanyCode | Lowercase |

- Truncated (true or false, depending on whether all the data is displayed or not)


# **getRecipientMasterData**
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


