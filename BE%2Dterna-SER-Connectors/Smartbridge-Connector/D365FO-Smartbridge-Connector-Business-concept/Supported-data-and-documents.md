The current version of the connector supports the archiving of the following data and documents:

| **Entity** | **Description** | **Purpose** | **Trigger for automatic synchronisation** |
|-- |--|--|--|
| **Vendors** | Includes: Vendor main data, Vendor primary addresses, Vendor primary contact information.            Usually available through data entities: Vendors, Vendors V2, etc. in D365FO. | Creating Doxis Folders | Insert/Update of data in D365FO |
| **Customers** | Includes: Customer main data, Customer primary addresses, Customer primary contact information.Usually available through data entities: Customers, Customers V2, etc. in D365FO. | Creating Doxis Folders | Insert/Update of data in D365FO |
| **Purchase orders** | Usually available through data entity: Purchase order headers in D365FO. | Creating Doxis Folders | Insert/Update of data in D365FO |
| **Sales orders** | Usually available through data entity: Sales order headers in D365FO. | Creating Doxis Folders | Insert/Update of data in D365FO |
| **Purchase order confirmations** | Usually available through data entity: entity Purchase order confirmation headers in D365FO. | Creating Doxis Files out of the default PO confirmation report  | Confirmation of a Purchase order |
|**Sales order confirmations**  | Usually available through data entity: Sales order confirmation headers in D365FO. | Creating Doxis Files out of the default PO confirmation report | Confirmation of a Sales order |
