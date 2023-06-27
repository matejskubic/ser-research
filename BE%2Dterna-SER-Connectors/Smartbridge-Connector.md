# 5.1 D365FO Smartbridge Connector Configuration

To have a working D365FO Smartbridge Connector in D365FO several configuration parameters must be defined:
* D365FO business events and endpoints configuration
* Doxis Smartbridge Data and document configuration
## 5.1.1 D365FO business events and endpoints configuration
Notifications send out of D365FO to Doxis Smartbridge are based on [D365FO Business events](https://learn.microsoft.com/en-us/dynamics365/fin-ops-core/dev-itpro/business-events/home-page).

The process requires to:
* Set up the D365FO Doxis endpoint
* Activate D365FO Smartbridge connector business event

_5.1.1.1 D365FO Smartbridge endpoint configuration_
To define the destination of Doxis Smartbridge solution where notifications from Business events are send to, a new type of endpoint is available: **Doxis smartbridge endpoint.**

To set up a new **Doxis smartbridge endpoint** you must:
1. On the **Business events** page, on the **Endpoints** tab, select **New** to create an endpoint.
2. Enter new value for endpoint **Name**.
3. In the **Configure new endpoint** dialog box, in the **Endpoint type** field, select the **Doxis smartbridge endpoint** type.
4. Enter new value for endpoint **Description.**
5. Enter new value for the endpoint **Authentication url.**
6. Enter new value for the **Request url**: enter the main url for Doxis Smartbridge services.
7. Enter values for **Request headers**.
8. Enter values for **Doxis Username**.
9. Enter values for **Doxis Password**.
10. Enter value for **Doxis Login Url**.

_5.1.1.2 D365FO Smartbridge connector business events_

D365FO Smartbridge connector introduces only one Business event named **SER_Doxis_SmartBridge_BusinessEvent**, which is a generic business event that is triggered for each document or data that is configured within the Doxis Smartbridge Data and document configuration.

For achieving an automatic document and data synchronization the business event **SER_Doxis_SmartBridge_BusinessEvent**  must be activated for a selected legal entity (All about Business events and this type of integration in D365FO can be found on [Microsoft official web documentation](https://learn.microsoft.com/en-us/dynamics365/fin-ops-core/dev-itpro/business-events/home-page))

## 5.1.2 Doxis Smartbridge Data and document configuration

The process of archiving documents and data from D365FO into Doxis Smartbridge is based on data entities in D365FO. 

To set up Doxis Smartbridge Data and document configuration you must specify the following parameters:
1. Click **Organization administration > Doxis Smartbridge Integration > Doxis Smartbridge Configuration.** 
2. Select **New** to create a new configuration. 
3. Enter **Target Entity**: select a data entity from the drop-down list that provides data you want to archive to Doxis Smartbridge (in this step Entity Root Table will be filled automatically)
4. Enter **Smartbridge Endpoint**: select the Doxis Smartbridge endpoint that was previously configured.
5. Enter parameters for archiving data and documents as Workspaces in Doxis Smartbridge:
   * **Smartbridge Workspace Url suffix**: enter the suffix for a specific Doxis Smartbridge workspace (e.g. /CubeFolder/CustomerWS)
   * **Smartbridge Workspace Url Configurator**: enter url template for reaching Doxis Smartbridge Workspace directly from D365FO. This url template is used to create direct links from an entity (e.g. specific customer) in D365FO to Doxis Smartbridge Workspace.
6. Enter parameters for archiving document printouts as Files in Doxis Smartbridge:
   * **Smartbridge File Url suffix**: enter the suffix for a specific Doxis Smartbridge workspace service (e.g. /CubeFolder/CustomerWS).
   * **Smartbridge File Url Configurator**: enter url template for reaching Doxis Smartbridge File directly from D365FO. This url template is used to create direct links from an entity (e.g. specific purchase order) in D365FO to Doxis Smartbridge File.



**____________________________________________________________________________________________________________________________________________________________________________________________________**
**NOTE**: it is mandatory to define one of the values above (either Smartbridge Workspace Url suffix or Smartbridge File Url suffix).
**____________________________________________________________________________________________________________________________________________________________________________________________________**


7. Enter **Filter**: define filter for querying data when triggering initial synchronization job. The filter configuration is used only when the synchronisation is run in the Initial (mass) synchronisation mode (see details in 5.2.1 Synchronisation/archiving modes).
8. Enter Doxis – F&O attributes mappings:
   * The mapping definition is based on a DotLiquid template definition.
   * Template:
{
	"<field_in_doxis>": "{{<Entity>.<Entity_Field>}}",
	"<field_in_doxis>": "<any_value>"
}

      In curly brackets, we will define which entity field corresponds to a certain data field in Doxis Smartbridge Service definition (Swagger). 

   * Example: mapping for sales order confirmation, where the Target Entity is SalesOrderConfirmationHeaderEntity
{
	"WSUniqueID": "{{SalesOrderConfirmationHeaderEntity.SalesOrderNumber}}",
	"ObjectSubject": "{{SalesOrderConfirmationHeaderEntity.ConfirmationNumber}}",
	"ObjectDate": "{{SalesOrderConfirmationHeaderEntity.ConfirmationDate}}",
	"DocumentType": "Sales order confirmation",
	"DocumentNumber": "{{SalesOrderConfirmationHeaderEntity.ConfirmationDocumentReference}}",
	"Sender": "{{SalesOrderConfirmationHeaderEntity.OrderTakerPersonnelNumber}}",
	"DocUniqueID": "{{SalesOrderConfirmationHeaderEntity.ConfirmationDocumentReference}}",
	"TargetNodeCode": "CoreDocuments"
}

The configuration also includes some validations for the DotLiquid definition:
* When Json format is not correct, the following error is raised: _“Not correct format on attributes mappings.”_
* When some <Entity_Field> is missing in Attributes mappings, the following warning is displayed: 
_“Bad format for attribute <field_in_doxis>”_ on which specific field error occurred.
* When fields that are defined as mandatory on the Doxis Smartbridge side, an error is raised (e.g. _“Missing mandatory doxis attribute ‘WSUniqueID’ in Doxis F&O attributes and mappings.”_)

Important notes:
1. You can't specify Smartbridge Workspace Url Configurator without first specifying Smartbridge Workspace Url suffix.
2. You can't specify Smartbridge File Url Configurator without first specifying Smartbridge File Url suffix.
3. The value in the parameters **Smartbridge Workspace Url Configurator** and **Smartbridge File Url Configurator** must be provided by Doxis Smartbridge solution implementation partner. 

The data and document configuration can be exported from or imported to D365FO either through Data management or Open in Excel option. This process is managed by using a data entity: **Doxis Smartbridge configuration.**


# 5.2 D365FO Smartbridge Connector Business concept
## 5.2.1 Synchronisation/archiving modes
When the configuration is defined, the data and document synchronization between D365FO and Doxis can run in three modes:
* **Automatically**: this option is enabled, when the business event SER_Doxis_SmartBridge_BusinessEvent is active and linked to an endpoint of the Doxis smartbridge endpoint type and a mapping configuration for an entity that is supported within this connector exists.
* **Manually**: this option is enabled when a mapping for a selected data entity is defined. User can trigger a manual synchronization directly from the form displaying data for a selected data entity. The manual synchronization is triggered by clicking the button **Transfer to Doxis**, which is displayed on selected forms in D365FO  (according to user security roles). The manual synchronization is supported only for data and documents that are represented in Doxis Smartbridge as Workspaces.

![wiki slika.png](/.attachments/wiki%20slika-2ad77d5d-fd95-4eee-a4ad-ddb596c31209.png)

* **Initial (mass) synchronization**: this option enables the initial transferring of all already existing documents and data in D365FO to Doxis Smartbridge when the connector is configured for the first time. 

**____________________________**

“Transfer to Doxis” button is currently available on the following forms:
* Accounts payable > Vendors > All vendors > Vendor > Doxis > Transfer to Doxis
* Accounts payable > Purchase orders > All purchase orders > Purchase order > Doxis -> Transfer to Doxis
* Accounts receivable > Customers > All customers > Customer > Doxis > Transfer to Doxis
* Accounts receivable > Orders > All sales orders > Sales order > Doxis > Transfer to Doxis

**____________________________________________________________________________________________________________________________________________________________________________________________________**

To run the initial synchronization, you must go to **Organization administration > Doxis Smartbridge Integration > Doxis Data Sync.** It is recommended that the initial synchronization is triggered as a batch job to run in the background.
The initial synchronization job runs the synchronization of all data and documents that are configured in 5.1.2 Doxis Smartbridge Data and document configuration according to the filtering parameters defined per each data entity.

## 5.2.2 Accessing Doxis Smartbridge Workspaces and documents directly from D365FO

When a synchronisation of specific data is triggered from D365FO, a business event is launched for a specific entity and a call to Doxis is created. The business event call to Doxis transfers data from the entity to the entity defined in the Doxis side, the data is mapped as we specified in the configuration in the **Doxis - F&O attributes mappings** field.
After the entity has been created and after the data has been successfully sent to Doxis, an attachment in D365FO will be created. The document type of the attachment depends on the Doxis Smartbridge configuration for the selected entity:
* When the configuration specifies the “Workspace” parameters, then an attachment of the type Doxis Workspace will be created.
* When the configuration specifies the “File” parameters, then an attachment of the type Doxis File will be created and also an attachment of the type Doxis Workspace will be created.

By clicking on the Open button in the Attachments form, a new web page will be opened with a direct link to the Doxis workspace or document. The page can only be accessed by a user that has accessing rights in Doxis Smartbridge application.

## 5.2.3 Supported data and documents

The current version of the connector supports the archiving of the following data and documents:

| **Entity** | **Description** | **Purpose** | **Trigger for automatic synchronisation** |
|-- |--|--|--|
| **Vendors** | Includes: Vendor main data, Vendor primary addresses, Vendor primary contact information.            Usually available through data entities: Vendors, Vendors V2, etc. in D365FO. | Creating Doxis Folders | Insert/Update of data in D365FO |
| **Customers** | Includes: Customer main data, Customer primary addresses, Customer primary contact information.Usually available through data entities: Customers, Customers V2, etc. in D365FO. | Creating Doxis Folders | Insert/Update of data in D365FO |
| **Purchase orders** | Usually available through data entity: Purchase order headers in D365FO. | Creating Doxis Folders | Insert/Update of data in D365FO |
| **Sales orders** | Usually available through data entity: Sales order headers in D365FO. | Creating Doxis Folders | Insert/Update of data in D365FO |
| **Purchase order confirmations** | Usually available through data entity: entity Purchase order confirmation headers in D365FO. | Creating Doxis Files out of the default PO confirmation report  | Confirmation of a Purchase order |
|**Sales order confirmations**  | Usually available through data entity: Sales order confirmation headers in D365FO. | Creating Doxis Files out of the default PO confirmation report | Confirmation of a Sales order |


## 5.2.4 Security
D365FO Smartbridge connector introduces two new roles for managing the connector’s functionalities:
* **Doxis Manager**: this role enables users to:
  * access and update Doxis Smartbridge Data and document configuration (5.1.2 Doxis Smartbridge Data and document configuration ),
  * trigger manual synchronization via button **Transfer to Doxis**,
  * trigger initial synchronization via batch job **Doxis Data Sync.**
* **Doxis Clerk**: this role enables users to trigger the manual synchronization via button **Transfer to Doxis.**

D365FO Smartbridge connector includes several separated duties that can be included in standard or custom-made roles used by a company:
* Doxis transfer customer 
* Doxis transfer vendor
* Doxis transfer purchase order 
* Doxis transfer sales order

## 5.2.5 Telemetry
D365FO Smartbridge connector also includes a telemetry monitoring of the synchronizations performed through the connector, tracking minimal request data (time, sender, etc.).  
This functionality can be extended also for error diagnostic if necessary. In this case, the user must:
* First enable the standard D365FO feature **Monitoring and Telemetry** in D365FO Feature management when it is not enabled yet.
* Go to **System administration > Setup > Monitoring and telemetry parameters.**
* Under **BeTelemetry** tab define the size of the message content that should be monitored (by default this is set to 0, meaning: no content message is monitored).















