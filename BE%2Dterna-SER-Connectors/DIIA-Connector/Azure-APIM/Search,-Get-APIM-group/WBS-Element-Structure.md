# Target data entity: `data/ProjectWBSDrafts`

#_API Methods_

##`POST`**/searchWBSElement**
Returns all open WBS (work breakdown structure) elements for the specified company code and the current date.

## Inbound data

_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. If it's not set, 100 records are retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| CompanyCode | dataAreaId | Mandatory parameter. <span style='color:red'>As per the documentation in Swagger, this parameter should not exist, data area Id should be queried through the _data -> Id_ parameter only.</span> |
| Id | <ul><li>dataAreaId</li><li>ProjectId</li><li>WBSId</li><li>Task</li></ul> | Mandatory parameter. It can be specified two ways: <ul><li>As a pipe delimited string that converts to an array with the elements listed in the Destination column. All the elements of the array are used for filtering, with the logical AND between them. </li><li>As a single value that contains an asterisk (*) as a wildcard character. In this case, the records will be retrieved if any of the fields listed in the Destination column match the entered text with the asterisk replacing any number of characters.</li></ul> If this value is not in any of these two formats, no records will be retrieved.|
| Asset | | <span style='color:red'>Not implemented</span> |
| CostCenter | | <span style='color:red'>Not implemented</span> |
| Custom1 - Custom20 | | <span style='color:red'>Not implemented</span> |
| Date | StartDate | Optional parameter |
| Description | Description | Optional parameter |
| GLAccount | | <span style='color:red'>Not implemented</span> |
| InternalOrder | ProjectId | |
| Manager | | <span style='color:red'>Not implemented</span> |
| ManagerNumber | | <span style='color:red'>Not implemented</span> |
| Project | Task | |

## Outbound data (searchWBSElementResponse)
_The response is in the following format:_
- SearchResult - JSON array with the following fields:

| Source | Destination | Comment |
|--|--|--|
| dataAreaId\|ProjectId\|WBSId\|Task | Id | Pipe-concatenated string containing the values from the 4 fields listed in the column _Source_. |
| dataAreaId | CompanyCode |
| StartDate | Date | Displayed in the format "yyyy-MM-dd"<br />Note: this Date parameter is not actually implemented in the filtering. | 
| | Description | |
| | Manager | |
| | ManagerNumber | |
| | Project | |
- Truncated (true or false, depending on whether all the data is displayed or not)

# Target data entity: `data/ProjectWBSDrafts`

#_API Methods_

##`POST`**/getWBSElement**
Checks whether the requested work breakdown structure element (WBS) exists and, if so, returns the corresponding details.

## Inbound data

_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. If it's not set, 100 records are retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| CompanyCode | dataAreaId | Mandatory parameter |
| Id | <ul><li>dataAreaId</li><li>ProjectId</li><li>WBSId</li><li>Task</li></ul> | Optional parameter. If it's specified, it has to be a pipe delimited string that converts to an array with the elements listed in the Destination column. All the elements of the array are used for filtering, with the logical AND between them. |

## Outbound data (getWBSElementResponse)
_If the API call is successful, the response is as a single JSON object with the following mapping:_
| Source | Destination | Comment |
|--|--|--|
| dataAreaId\|ProjectId\|WBSId\|Task| Id | A pipe-delimited string consisting of the 4 fields from the OData entity, concatenated. |
| Note | Description |
| WorkerResponsiblePersonnelNumber | ManagerNumber | This value is obtained from the sub-entity named "Projects". | 
| Project | Task | |
