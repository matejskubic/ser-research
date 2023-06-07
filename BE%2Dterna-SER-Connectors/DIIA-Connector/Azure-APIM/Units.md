# Target data entity: `data/UnitsOfMeasure`

#_API Methods_

##`POST`**/getUnits**
Evaluates the locale of the session and returns the corresponding units supported by the ERP system and their descriptions.

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