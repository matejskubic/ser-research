When the configuration is defined, the data and document synchronization between D365FO and Doxis can run in three modes:
* **Automatically**: this option is enabled, when the business event SER_Doxis_SmartBridge_BusinessEvent is active and linked to an endpoint of the Doxis smartbridge endpoint type and a mapping configuration for an entity that is supported within this connector exists.
* **Manually**: this option is enabled when a mapping for a selected data entity is defined. User can trigger a manual synchronization directly from the form displaying data for a selected data entity. The manual synchronization is triggered by clicking the button **Transfer to Doxis**, which is displayed on selected forms in D365FO  (according to user security roles). The manual synchronization is supported only for data and documents that are represented in Doxis Smartbridge as Workspaces.

![wiki slika.png](/.attachments/wiki%20slika-2ad77d5d-fd95-4eee-a4ad-ddb596c31209.png)

* **Initial (mass) synchronization**: this option enables the initial transferring of all already existing documents and data in D365FO to Doxis Smartbridge when the connector is configured for the first time. To run the initial synchronization, you must go to **Organization administration > Doxis Smartbridge Integration > Doxis Data Sync.** It is recommended that the initial synchronization is triggered as a batch job to run in the background.
The initial synchronization job runs the synchronization of all data and documents that are configured in 5.1.2 Doxis Smartbridge Data and document configuration according to the filtering parameters defined per each data entity.

**____________________________**

“Transfer to Doxis” button is currently available on the following forms:
* Accounts payable > Vendors > All vendors > Vendor > Doxis > Transfer to Doxis
* Accounts payable > Purchase orders > All purchase orders > Purchase order > Doxis -> Transfer to Doxis
* Accounts receivable > Customers > All customers > Customer > Doxis > Transfer to Doxis
* Accounts receivable > Orders > All sales orders > Sales order > Doxis > Transfer to Doxis
* Sales and marketing > Relationships > Opportunities > All opportunities > Opportunity > Doxis > Transfer to Doxis
* Sales and marketing > Sales quotations > All quotations > Sales quotation > Doxis > Transfer to Doxis


**_________________________________**

