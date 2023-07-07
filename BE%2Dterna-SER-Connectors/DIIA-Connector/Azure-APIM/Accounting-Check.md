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

## Outbound data (checkAccountingResponse)
_The processed inbound data is sent to the API service at the URL BESer_Services/SERInvoiceService/CheckAccounting, and the response from there is a single JSON object with the following format:_

| Source | Destination  | Comment |
|--|--|--|
| | Fields | JSON object with the structure described in the table below. (**) |
| | Valid | The validation result. If all the elements from the Fields object are valid, the value here will be _true_. Otherwise, it will be _false_. |
| | Code | Validation code |3
| | Message | Validation message |

<span style="font-weight: normal">(*****)</span> <b>_Fields_ object structure</b>
All the elements of the Fields object are with the same structure, and their structure is described in the table labeled Fields elements' object structure (***).
| Source | Destination | Comment |
|--|--|--|
| | Asset | JSON object |
| | CostCenter | JSON objects with the structure described below (***) |
| | Type | Message type |

