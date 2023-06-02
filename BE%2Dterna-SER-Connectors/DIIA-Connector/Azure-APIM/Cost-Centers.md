# Target data entity: `data/CostCenters`

#_API Methods_

## **searchCostCenters**
Returns all open cost centers for the specified company code and the current date.

## Inbound data

_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. If it's not set, 100 records are retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| Id | OperatingUnitNumber | Optional parameter |
| Name | Description | Optional parameter |

## Outbound data (searchCostCentersResponse)
_The response is in the following format:_
- SearchResult - JSON array with the following fields:

| Source | Destination | Comment |
|--|--|--|
| OperatingUnitNumber | Id| |
|  | CompanyCode | <div style="color:maroon">This seems to be the value passed as an input parameter, although the parameter is not implemented in the filtering.</div> |
| | Date | Current date in the "yyyy-MM-dd" format.| 
| Name| Description | |
- Truncated (true or false, depending on whether all the data is displayed or not)

# **getCostCenter**
Returns open cost centers.
## Inbound data
_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. Unnecessary here, as only one record is eventually retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| Id | OperatingUnitNumber | Mandatory parameter |

## Outbound data (getCostCenterResponse)
_The response is a single JSON object with the following format:_
| Source | Destination | Comment |
|--|--|--|
| OperatingUnitNumber | Id| |
| Name| Description | |

