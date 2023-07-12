# Target data entity: `Any existing data entity. The data entity name is one of the inbound parameters`

#_API Method_

Unlike all the other methods from this API Management, the parameters for these methods are sent 

##`GET` **/data/{EntityName}**
Retrieves data from F&O through the specified data entity.

## Inbound data
| Parameter name| Parameter type | Comment |
|--|--|--|
| EntityName | Template parameter (string) | Mandatory |
| $top | Query parameter (int) | Optional |
| $filter | Query parameter (string) | Optional |
| $select | Query parameter (string) | Optional |
| $orderby | Query parameter (string) | Optional |
| cross-company | Query parameter (boolean) | Optional |

An example of this APIM call (from Postman) would be:
{{apiUrl}}/data/FiscalPeriods?$top=2&$select=Calendar,FiscalYear
It would query the _FiscalPeriods_ data entity and retrieve values from the _Calendar_ and _FiscalYear_ fields from the first two records.

## Outbound data
_Outbound data is a JSON object, with one element named SearchResult, which is a JSON array. The structure of this array's elements depends on the specified data entity and the fields that need to be retrieved._

##`POST` **/data/{EntityName}**
Inserts a new record in the specified data entity.

## Inbound data
_The Inbound data consists of the data entity name in the URL, and the JSON object containing all the necessary elements of a single record from the data entity._

## Outbound data
_If the record is successfully inserted, the response body is a JSON object that contains the whole inserted record, preceded by two elements named @odata.context and @odata.etag._


##`PATCH` **/data/{EntityName}(unique_record_identifier)**
Updates the specified record in the specified data entity.

## Inbound data
_The Inbound data consists of the entity name, followed by the field values needed for uniquely identifying a single record from the data entity in the URL, and a JSON object containing all the fields that need to be updated, with their new values. An example of the inbound data from Postman would be:_
URL:
{{apiUrl}}/data/CustomerGroups(dataAreaId='usmf',CustomerGroupId='tes-t005')?cross-company=true
Body:
{
    "Description": "testing Patch via Postman"
}

## Outbound data (searchAssetsResponse)
_If the record is successfully updated, the response comes with an empty body and the status code 204._