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
_Outbound data is a JSON object, with one element named SearchResult, which is a JSON array. The structure of this array'e elements depends on the specified data entity and the fields that need to be retrieved._

##`POST` **/data/{EntityName}**
Retrieves data from F&O through the specified data entity.

## Inbound data


| Parameter name| Parameter type | Comment |
|--|--|--|
| EntityName | Template parameter (string) | Mandatory |
| $top | Query parameter (int) | Optional |
| $filter | Query parameter (string) | Optional |
| $select | Query parameter (string) | Optional |
| $orderby | Query parameter (string) | Optional |
| cross-company | Query parameter () | Optional |

## Outbound data (searchAssetsResponse)
_The response is a list of elements from the specified data entity that satisfies the filtering criteria._