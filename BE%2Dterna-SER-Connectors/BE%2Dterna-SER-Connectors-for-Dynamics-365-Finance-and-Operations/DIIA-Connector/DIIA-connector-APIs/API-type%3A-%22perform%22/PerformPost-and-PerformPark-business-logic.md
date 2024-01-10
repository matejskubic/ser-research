Under construction


::: mermaid
flowchart TD
    SER --> performPark
    SER --> performPost
    performPark-->Method{PostingMetod?}
    performPost-->Method
    Method-->pendingInvoice
    Method-->journal
    pendingInvoice-->SERInvoiceService
    journal-->SERInvoiceService
    SERInvoiceService-->VendorInvoiceHeaderEntity
    SERInvoiceService-->VendInvoiceJournalHeaderEntity
    performPark-.->performLink
    performPost-.->performLink
    performLink-->linkMethod{PostingMethod?}
    linkMethod--pendingInvoice-->BESer_VendorInvoiceDocumentAttachements
    linkMethod--journal-->BESer_PostedVendorInvoiceDocumentAttachements
:::
