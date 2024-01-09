# Target data entity: `data/VendorProductDescriptionsV2`

#_API Methods_

##`POST`**/searchExternalItemNumbers**
Determines all open cost centers for the current company code and the current date.

## Inbound data

_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. If it's not set, 100 records are retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| CompanyCode | dataAreaId | Mandatory parameter |
| Id | VendorProductNumber | Optional parameter |
| Description | VendorProductDescription | Optional parameter |
| VendorId | VendorAccountNumber | Optional parameter |

## Outbound data (searchExternalItemNumbersResponse)
_The response is in the following format:_
- SearchResult - JSON array with the following fields:

| Source | Destination | Comment |
|--|--|--|
| dataAreaId | CompanyCode |
| VendorAccountNumber | VendorId | |
| ItemNumber | ItemNumber | |
| VendorProductNumber | Id | |
| VendorProductDescription & VendorABCCodeNote | Description | The two fields from the source data entity concatenated, with a space separating them. |
- Truncated (true or false, depending on whether all the data is displayed or not)
