# D365FO Target data entity: `data/VendorPaymentMethods`

#_API Methods_

##`POST`**/getPaymentMethods**
Returns valid payment methods.

## Inbound data

_A JSON/XML object with the following items:_
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| CompanyCode | dataAreaId | Mandatory parameter |

## Outbound data (getPaymentMethodsResponse)
_The response is in the following format:_
- SearchResult - JSON array with the following fields:

| Source | Destination | Comment |
|--|--|--|
| Name | Id | |
| Description | Description | |