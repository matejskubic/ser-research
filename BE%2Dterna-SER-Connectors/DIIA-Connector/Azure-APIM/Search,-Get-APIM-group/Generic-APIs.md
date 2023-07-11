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
| cross-company | Query parameter () | Optional |

## Outbound data (searchAssetsResponse)
_The response is a list of elements from the specified data entity that satisfies the filtering criteria._