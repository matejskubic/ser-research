#_API Methods_

# Target data entity: `data/MainAccountCompanies`

## **searchGLAccounts**
Returns a list with basic information about the GL accounts for the passed filtering criteria.

## Inbound data

_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. If it's not set, 100 records are retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| CompanyCode | LegalEntityId | Mandatory parameter | 
| Id | MainAccountId | Optional parameter |
| Description | Name | Optional parameter |

## Outbound data (searchGLAccountsResponse)
_The response is in the following format:_
- SearchResult - JSON array with the following fields:

| Source | Destination | Comment |
|--|--|--|
| MainAccountId | Id |
| LegalEntityId| CompanyCode | Lowercase |
| | Date | If the Date value is passed in the parameters, that value is shown; otherwise, the current date is shown. The value is displayed in the format "yyyy-MM-dd"<br />Note: this Date parameter is not actually implemented in the search criteria. |
- Truncated (true or false, depending on whether all the data is displayed or not)


# Target data entity: `data/MainAccountLegalEntities`

# **getGLAccount**
Returns the first open or active G/L account information.
## Inbound data
_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. Unnecessary here, as only one record is eventually retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| CompanyCode | LegalEntityId | Mandatory parameter | 
| Id | MainAccountId | Optional parameter |
| Date | ActiveFrom - ActiveTo | If this parameter is specified, only the records whose ActiveFrom value is before or on the Date parameter value, and whose ActiveTo value is either empty or not before the Date parameter value will be shown |

## Outbound data (getGLAccountResponse)
_The response as a single JSON object with the following format:_
| Source | Destination | Comment |
|--|--|--|
| MainAccountId| Id| |
| MainAccountId | Description|