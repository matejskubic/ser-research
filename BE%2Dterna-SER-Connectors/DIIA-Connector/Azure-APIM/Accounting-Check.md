#_API Methods_

## **checkAccounting**
Check of account assignment data for invoices without a purchase order reference.

## Inbound data

_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. If it's not set, 100 records are retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| CompanyCode | dataAreaId | Mandatory parameter |
| DocumentDate | |
| Positions | | Mandatory parameter. JSON array containing objects with the structure described in the table below. (*) |
| RecipientId | | |
| Type | | |
| VendorId | | |
| Date | | |

(*) <b>Positions item object structure</b>
| Source | Destination | Comment |
|--|--|--|
| Id| | |
| Type | |
| Asset | |
| CostCenter | | |
| ExternalItemNumber | |
| Custom1 - Custom20| | <span style="color:red">Not implemented</span> |
| GLAccount | | |
| InternalOrder | | |
| RAType | | |
| WBSElement| | |

## Outbound data (checkPostingResponse)
_The processed inbound data is sent to the API service at the URL BESer_Services/SERInvoiceService/CheckAccounting, and the response from there is a single JSON object with the following format:_
| Source | Destination  | Comment |
|--|--|--|
| | Result| JSON array with just one element, whose structure is described in the table below. (*) |

(*) <b>Result item object structure</b>
| Source | Destination | Comment |
|--|--|--|
| | Code | Error code, if an error is detected during the checking |
| | Message | Error message, if an error is detected during the checking |
| | Type | Message type |