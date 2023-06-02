# Target data entity: `data/ProjectWBSDrafts`

#_API Methods_

## **getWBSElement**
Checks whether the requested work breakdown structure element (WBS) exists and, if so, returns the corresponding details.

## Inbound data

_The data is sent as a JSON object with the following mapping:_
| Source | Destination | Comment |
|--|--|--|
| CompanyCode | dataAreaId | Mandatory parameter |
| Id | FixedAssetNumber | Optional parameter. If it's specified, it has to be a pipe delimited string that converts to an array with the following elements:<ul><li>dataAreaId</li><li>ProjectId</li><li>WBSId</li><li>Task</li></ul>All the elements of the array are used for filtering, with the logical AND between them. |

## Outbound data (getWBSElementResponse)
_If the API call is successful, the response arrives as a single JSON object with the following mapping:_
| Source | Destination | Comment |
|--|--|--|
| dataAreaId\|ProjectId\|WBSId\|Task| Id | A pipe delimited string consisting of the 4 fields from the OData entity, concatenated.|
| Note | Description |
| WorkerResponsiblePersonnelNumber | ManagerNumber | This value is obtained from the sub-entity named "Projects". | 
| Project | Task | |