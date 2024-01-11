# D365FO Target service: `/api/services/BESer_Services/SERInvoiceService/CheckPosting`

#_API Methods_

##`POST` **/checkPosting**
Checks the invoice data for consistency.

## Inbound data

_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. If it's not set, 100 records are retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| CompanyCode | dataAreaId | Mandatory parameter |
| Data | | Mandatory parameter. JSON object with the structure described in the table below. (*) |

(*) <b>Data object structure</b>
| Source | Destination | Comment |
|--|--|--|
| Amount | | | JSON object with the structure described in the table below. (**)  |
| Date | Date | |
| OrderType | | |
| Positions | | JSON array with the elements whose structure is described in the table below. (***) |
| RecipientId | | |
| Type | | |
| VendorId | VendorAccount | |
| BankId | BankAccount | |
| ERP | | |
| Number | InvoiceNumber | |
| RecipientTransferTo | | |
| RecipientVATNumber | | |
| SCBIndicator | | |
| SubsequentDebit | | |
| TermsOfPayment | | |
| Text | InvoiceDescription | |
| VendorOneTime | | JSON object with the structure described in the table below. (****) |
| VendorTransferFrom | | |
| VendorVATNumber | | |
| PaymentMethod | MethodOfPayment | |
| ESRReferenceNumber | | |

(**) <b>Amount object structure</b>
| Source | Destination | Comment |
|--|--|--|
| Currency | Currency | |
| Gross | | |
| GrossDiscount | TotalDiscount | |
| GrossTotal | | |
| Net | | |
| Tax | | |

(***) <b>Positions object structure</b>
| Source | Destination | Comment |
|--|--|--|
| NetUnit | UnitPrice | |
| Quantity | ReceiveNow | |
| Tax | | |
| TaxCode | | |
| TaxRate | | |
| Type | | |
| Unit | | |
| Asset | | |
| CostCenter | | |
| ExternalItemNumber | | |
| Custom1 - Custom20 | | |
| Description | LineDescription | |
| GLAccount | GLAccount | Not used for direct save instead used by F&O service to create offset dimension |
| GRDeliveryNoteNumber | | |
| GRId | | |
| GRPosition | | |
| GRType | | |
| InternalOrder | | |
| OrderId | PurchaseOrder | |
| PositionId | PurchLineNumber | |
| Text | ItemName | |
| Total | NetAmount / Credit | Depending on the posting method (pendingInvoice or journal) specified in the request |
| Custom1 | ItemNumber | | |
| WBSElement | | |

(****) <b>VendorOneTime object structure</b>
| Source | Destination | Comment |
|--|--|--|
| City | | |
| Country | | |
| Name | | |
| Street | | |
| ZIP | | |
| BIC | | |
| BankAccountNumber | | |
| BankCode | | |
| BankCountry | | |
| BankName | | |
| IBAN | | |
| Name2 | | |
| TaxNumber | | |

## Outbound data (checkPostingResponse)
_The response is a single JSON object with the following format:_
| Source | Destination  | Comment |
|--|--|--|
| | Result| JSON array with just one element, whose structure is described in the table below. (*) |

(*) <b>Result item object structure</b>
| Source | Destination | Comment |
|--|--|--|
| | Code | Error code, if an error is detected during the checking |
| | Message | Error message, if an error is detected during the checking |
| | Type | Message type |