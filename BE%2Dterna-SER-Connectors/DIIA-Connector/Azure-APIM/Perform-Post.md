# Target data entities: `data/TaxGroupDatas`, `data/TaxItemGroups`

#_API Methods_

##`POST`**/performPost**
Post an invoice or credit memo.

## Inbound data

_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. If it's not set, 100 records are retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Data entity | Comment |
|--|--|--|--|
| CompanyCode | dataAreaId | TaxGroupDatas, TaxItemGroups | Mandatory parameter |
| Data | | | Mandatory parameter. JSON object with the structure described in the table below. (*) |
| | Date | | |
| | Document | | Optional parameter. JSON object with the structure described in the table below. (*****) |

(*) <b>Data object structure</b>
| Source | Destination | Data entity | Comment |
|--|--|--|--|
| Amount | | | JSON object with the structure described in the table below. (**)  |
| Date | | | |
| OrderType | | | |
| Positions | | | JSON array with the elements whose structure described in the table below. (***) |
| RecipientId | | | |
| Type | | | |
| VendorId | | | |
| BankId | | | |
| ERP | | | |
| Number | | | |
| RecipientTransferTo | | | |
| RecipientVATNumber | | | |
| SCBIndicator | | | |
| SubsequentDebit | | | |
| TermsOfPayment | | | |
| Text | | | |
| VendorOneTime | | | JSON object with the structure described in the table below. (****) |
| VendorTransferFrom | | | |
| VendorVATNumber | | | |
| PaymentMethod | | | |
| ESRReferenceNumber | | | |

(**) <b>Amount object structure</b>
| Source | Destination | Data entity | Comment |
|--|--|--|--|
| Currency | | | |
| Gross | | | |
| GrossDiscount | | | |
| GrossTotal | | | |
| Net | | | |
| Tax | | | |

(***) <b>Positions object structure</b>
| Source | Destination | Data entity | Comment |
|--|--|--|--|
| NetUnit | | | |
| Quantity | | | |
| Tax | | | |
| TaxCode | | | |
| TaxRate | | | |
| Type | | | |
| Unit | | | |
| Asset | | | |
| CostCenter | | | |
| ExternalItemNumber | | | |
| Custom1 - Custom20 | | | |
| Description | | | |
| GLAccount | | | |
| GRDeliveryNoteNumber | | | |
| GRId | | | |
| GRPosition | | | |
| GRType | | | |
| InternalOrder | | | |
| OrderId | | | |
| PositionId | | | |
| Text | | | |
| Total | | | |
| WBSElement | | | |

(****) <b>VendorOneTime object structure</b>
| Source | Destination | Data entity | Comment |
|--|--|--|--|
| City | | | |
| Country | | | |
| Name | | | |
| Street | | | |
| ZIP | | | |
| BIC | | | |
| BankAccountNumber | | | |
| BankCode | | | |
| BankCountry | | | |
| BankName | | | |
| IBAN | | | |
| Name2 | | | |
| TaxNumber | | | |

(*****) <b>Document object structure</b>
| Source | Destination | Data entity | Comment |
|--|--|--|--|
| | Database| | |
| | DocumentId | | |
| | GUID | | |
| | IECM | | |
| | MimeType | | |
| | WebCube | | |
| | HCSId | | |

## Outbound data (performPostResponse)
_The response is a single JSON object with the following format:_
| Source | Destination | Data entity | Comment |
|--|--|--|--|
| | Id| |
| | Date | | |
| | Number | | |
| | FiscalYear | | |
| | Period | | |
