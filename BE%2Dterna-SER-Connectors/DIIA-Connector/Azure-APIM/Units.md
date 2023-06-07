# Target data entity: `data/UnitsOfMeasure`

#_API Methods_

##`POST`**/getUnits**
Returns all assets for the specified company code and the current date.

## Inbound data

_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. If it's not set, 10 records are retrieved.
- data. The sub-object that, as per the specification should contain only 1 sub-item named Date, but none of it is implemented, and in fact, is not needed.

## Outbound data (getUnitsResponse)
_The response is in the following format:_
- Result - JSON array with the following fields:

| Source | Destination | Comment |
|--|--|--|
| UnitSymbol | Id| |
| UnitDescription | Description | |