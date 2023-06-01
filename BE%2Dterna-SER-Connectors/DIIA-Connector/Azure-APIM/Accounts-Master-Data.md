#_API Methods_

# Target data entity: `data/MainAccountCompanies`

## **searchGLAccounts**
Returns a list with basic information about the GL accounts for the passed filtering criteria.

## Inbound data

_The data is sent as a JSON object with the following mapping: _
| Source | Destination | Comment |
|--|--|--|
| CompanyCode | LegalEntityId | Lowercase | 
| Id | MainAccountId |
| Description | Name |

## Outbound data (searchGLAccountsResponse)
_The response arrives in the following format:_
- SearchResult - JSON array with the following fields:

| Source | Destination | Comment |
|--|--|--|
| MainAccountId | Id |
| LegalEntityId| CompanyCode | Lowercase |
| Date | | If Date value is passed in the parameters, that value is shown; otherwise, the current date is shown |
- Truncated (true or false, depending on whether all the data is displayed or not)


# Target data entity: `data/MainAccountLegalEntities`

# **getGLAccount**
Returns the first open or active G/L account information.
## Inbound data
_The data is sent as a JSON object with the following mapping:_
| Source | Destination | Comment |
|--|--|--|
| LegalEntityId | CompanyCode |
| Id | MainAccountId |
| Date | ActiveFrom - ActiveTo | If this parameter is specified, only the records whose ActiveFrom value is before or on the Date parameter value, and whose ActiveTo value is either empty or not before the Date parameter value will be shown |

## Outbound data (getGLAccountResponse)
_The response as a single JSON object with the following format:_
| Source | Destination | Comment |
|--|--|--|
| MainAccountId| Id| |
| MainAccountId | Description|