# Target data entity: `data/ExchangeRatesCDSEntity`

#_API Methods_

##`POST` **/searchExchangeRates**
Returns the currency exchange rates against the EUR for the current date.

## Inbound data

_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. If it's not set, 100 records are retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| Currency | _FromCurrencyCode_ or _ToCurrencyCode_| Optional parameter. If it's not supplied, conversion rates from and to EUR will be returned. |
| Date | ValidFrom - ValidTo | Mandatory parameter. The Date parameter value must be between the ValidFrom and ValidTo dates from the data entity. |

## Outbound data (searchAssetsResponse)
_The response is in the following format:_
- SearchResult - JSON array with the following fields:

| Source | Destination | Comment |
|--|--|--|
| Rate | Rate | |
| dataAreaId | CompanyCode |
| _FromCurrencyCode_ or _ToCurrencyCode_ | Currency | The currency . | 
| Name| Description | |
| FixedAssetGroupId | Category | |
- Truncated (true or false, depending on whether all the data is displayed or not)

