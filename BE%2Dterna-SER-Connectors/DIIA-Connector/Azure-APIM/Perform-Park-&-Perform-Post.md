# Target data entities: `data/TaxGroupDatas`, `data/TaxItemGroups`, `data/VendInvoiceJournalHeaderEntity` + `data/VendInvoiceJournalLineEntity` <span style="font-size:12pt">for posting method 'journal' or</span> `data/VendInvoiceJournalHeaderEntity` + `data/VendInvoiceJournalLineEntity` <span style="font-size:12pt">for posting method 'pendingInvoice'</span>

#_API Methods_

##`POST`**/performPost**
Post an invoice or credit memo.
 The performPost method's main objective is to post business documents of type _pending vendor invoice_ and invoice journal. The type of posted document is specified by the combination of values of the request attributes named _requestOrderType_ and _postingMethod_, the following way:
- if requestOrderType = "WIPO" OR requestOrderType = "WOPO" AND postingMethod = "pendingInvoice", the posting method will be "pendingInvoice"
- if requestOrderType = "WOPO" AND postingMethod = "journal", the posting method will be " journal".
- In case of any other combination of values of these input values, an error is thrown.

The final value is stored in the _postingMethodString_ context variable and used later in the code.

In order to fill the tax specification for each invoice line, the data entities TaxGroupDatas and TaxItemGroups are called from the back-end F&O system. The returned values are stored in corresponding JArray objects, and these values are used later in the code when each invoice line is processed.

The next step is defining the set-body policy in which the whole request body is defined and saved, and this is the biggest part of the policy code. The first job of the set-body policy section was to map the attributes from the SER request to the F&O backend service. In order to get a better understanding of what the backend request would look like a mockup request is shown below:

    "InvoiceRequest": {
        "Header": {
            "PostingMethod": "pendingInvoice",
            "dataAreaId": "demf"
        },
        "Lines": [
            {
                "LineNumber": "1",
                "UnitPrice": 100,
                "ReceiveNow": 1,
                "SalesTaxGroup": "AP-EU",
                "ItemSalesTax": "FULL",
                "ItemNumber": "SER-TEST2"
            },
            {
                "LineNumber": "2",
                "UnitPrice": 100,
                "ReceiveNow": 10,
                "SalesTaxGroup": "AP-EU",
                "CustomFieldMapping": {
                    "CustomFieldNames": [
                        "ItemSalesTax",
                        "ItemNumber"
                    ],
                    "CustomFieldValues": [
                        "FULL",
                        "SER-TEST2"
                    ]
                },
                "DimensionsData": {
                    "DimensionsNames": [
                        "CostCenter",
                        "BusinessUnit"
                    ],
                    "DimensionsValues": [
                        "007",
                        "005"
                    ]
                }
            }
        ]
    }



## Inbound data
_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. If it's not set, 100 records are retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Data entity | Comment |
|--|--|--|--|
| CompanyCode | dataAreaId | TaxGroupDatas, TaxItemGroups | Mandatory parameter |
| Data | | | Mandatory parameter. JSON object with the structure described in the table below. (*) |
| | Date | InvoiceDate | |
| | Document | | Optional parameter. JSON object with the structure described in the table below. (*****) |

(*) <b>Data object structure</b>
| Source | Destination | Data entity | Comment |
|--|--|--|--|
| Amount | | | JSON object with the structure described in the table below. (**)  |
| Date | Date | | |
| OrderType | | | |
| Positions | | | JSON array with the elements whose structure is described in the table below. (***) |
| RecipientId | | | |
| Type | | | |
| VendorId | VendorAccount | | |
| BankId | BankAccount | | |
| ERP | | | |
| Number | InvoiceNumber | | |
| RecipientTransferTo | | | |
| RecipientVATNumber | | | |
| SCBIndicator | | | |
| SubsequentDebit | | | |
| TermsOfPayment | | | |
| Text | InvoiceDescription | | |
| VendorOneTime | | | JSON object with the structure described in the table below. (****) |
| VendorTransferFrom | | | |
| VendorVATNumber | | | |
| PaymentMethod | MethodOfPayment | | |
| ESRReferenceNumber | | | |

(**) <b>Amount object structure</b>
| Source | Destination | Data entity | Comment |
|--|--|--|--|
| Currency | Currency | | |
| Gross | | | |
| GrossDiscount | TotalDiscount | | |
| GrossTotal | | | |
| Net | | | |
| Tax | | | |

(***) <b>Positions object structure</b>
| Source | Destination | Data entity | Comment |
|--|--|--|--|
| NetUnit | UnitPrice | | |
| Quantity | ReceiveNow | | |
| Tax | | | |
| TaxCode | | | |
| TaxRate | | | |
| Type | | | |
| Unit | | | |
| Asset | | | |
| CostCenter | | | |
| ExternalItemNumber | | | |
| Custom1 - Custom20 | | | |
| Description | LineDescription | | |
| GLAccount | GLAccount | | Not used for direct save instead used by F&O service to create offset dimension |
| GRDeliveryNoteNumber | | | |
| GRId | | | |
| GRPosition | | | |
| GRType | | | |
| InternalOrder | | | |
| OrderId | PurchaseOrder | | |
| PositionId | PurchLineNumber | | |
| Text | ItemName | | |
| Total | NetAmount / Credit | | Depending on the posting method (pendingInvoice or journal) specified in the request |
| Custom1 | ItemNumber | | | |
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
