# D365FO Target data entities: `data/TaxGroupDatas`, `data/TaxItemGroups`, `data/JournalNames`, `data/VendInvoiceJournalHeaderEntity` + `data/VendInvoiceJournalLineEntity` <span style="font-size:12pt">for posting method 'journal' or</span> `data/VendInvoiceJournalHeaderEntity` + `data/VendInvoiceJournalLineEntity` <span style="font-size:12pt">for posting method 'pendingInvoice'.</span>

#_API Methods_

##`POST`**/performPost**
 The performPost method's main objective is to post business invoice documents as _pending vendor invoices_ or _invoice journals_ in D365FO. The type of posted document is specified by the combination of values of the request attributes named _requestOrderType_ and _postingMethod_, the following way:
- if requestOrderType = "WIPO" OR requestOrderType = "WOPO" AND postingMethod = "pendingInvoice", the posting method will be "pendingInvoice"
- if requestOrderType = "WOPO" AND postingMethod = "journal", the posting method will be " journal".
- In case of any other combination of values of these input parameters, an error is thrown.

The final value is stored in the _postingMethodString_ context variable and used later in the code.

In order to fill the tax specification for each invoice line, the data entities TaxGroupDatas and TaxItemGroups are called from the back-end F&O system. The returned values are stored in corresponding JArray objects, and these values are used later in the code when each invoice line is processed.

The next step is defining the set-body policy in which the whole request body is defined and saved. This is the biggest part of the policy code, and because of the policy size limitation, it is moved to the policy fragment. The first job of the set-body policy section was to map the attributes from the SER request to the F&O backend service. In order to get a better understanding of what the backend request would look like a mockup request is shown below:

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
 It is required by the data contract that the request is sent as one JObject named _InvoiceRequest_, and that it contains another JObject named _Header_ and a JArray named _Lines_. As their names suggest, the first one contains all the invoice header data, and the other one all data invoice lines data. This _InvoiceRequest_ JObject is the output of the set-body code block.

In order to prepare the data for the InvoiceRequest JObject, the mapping functionality is applied using multiple dictionaries, each corresponding to a certain JObject inside the SER request. For example, a _positionsDict_ dictionary is used for mapping the order lines data. This mapping had to consider the exact names of the attributes from the targeting F&O data entities and map the input attributes with them accordingly.

After all the dictionaries for different request sections are specified, there is a section dealing with the invoice lines, which contains several other functionality implementations. One of them is custom financial dimensions mapping functionality, which works in a way so that custom attributes inside the request can be transformed into financial dimension information. A request header parameter named _posMapping_ was used for this purpose. It's a JSON value that contains the mapping information between the request name attribute and the financial dimension name from the backend system. If there are any dimensions, their values will be sent inside the request to the backend via the _DimensionsData_ JObject as shown in the request mockup above.

After the set-body policy is finished a newly defined request is sent to the F&O backend service to a method called _postVendInvoice_, which will save the request as a vendor pending invoice or invoice journal for which the service method code execution will differ, depending on which document is selected. For the invoice journal document, a _JournalBatchNumber_ attribute is checked to see if the specified journal number already exists, and if it doesn’t, it is created using the _createJournalHeader_ method. Next, if any line data is present, the method _createJournalLine_ will be executed for each subsequent line. The _VendInvoiceJournalHeaderEntity_ is used for the journal header, and for the journal line, the _VendInvoiceJournalLineEntity_ data entity is used.

A similar approach is used for pending vendor invoices but with different data entities. For the invoice header, the _VendorInvoiceHeaderEntity_ is used; for the invoice lines, the _VendorInvoiceLineEntity_ is used. What is also important is that all data that is saved inside F&O is returned to the API management service as a response, so that any additional checks or logic can be executed if needed.

 After the backend response is received inside the API management, a specific code section is executed before the request is returned to the client. This code is placed in the _outbound_ section. One detail that needs to be noted here is the special document attachment section, which is defined so that an attachment for that invoice document should be created if the request contains a JObject named _Document_. A method named _performLink_ is created in the API management for that purpose, and it's called from both the _performPark_ and _performPost_ methods with all necessary attributes passed to it.

Eventually, the request data is transformed into a response object as defined by SER and returned to the client.


##`POST`**/performPark**
The overall processing scope of this method is almost the same as for the _performPost_ method, with the main difference that the created document in D365FO is not posted. 
<br /><br />

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
