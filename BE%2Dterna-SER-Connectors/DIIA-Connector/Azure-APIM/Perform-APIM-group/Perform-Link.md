# Target data entity: `data/VendorInvoiceHeaders`, `data/BESer_VendorInvoiceDocumentAttachements`, `data/BESer_PostedVendorInvoiceDocumentAttachements`, `data/InvoiceJournalHeaderAttachments_BESer`

#_API Methods_

##`POST`**/performLink**
Links an attachment to an invoice that has already been posted. The method is called from the PerformPark and PerformPost methods, when a document needs to be attached to an invoice or credit memo.

## Inbound data

_A JSON/XML object with the following items:_
- maxHits. Optional parameter that indicates the number of records that need to be returned. If it's not set, 100 records are retrieved.
- data. The sub-object containing the data values with the mapping:

| Source | Destination | Comment |
|--|--|--|
| CompanyCode | dataAreaId | Mandatory parameter |
| Database | | |
| DocumentId | | |
| GUID | | |
| IECM | | |
| MimeType | | |
| Type | | |
| WebCube | | |
| Date | | |
| HCSId | | |

## Outbound data
There's outbound data from the method.