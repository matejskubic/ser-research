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
```json
	{
		"<field_in_doxis>": "{{<Entity>.<Entity_Field>}}",
		"<field_in_doxis>": "<any_value>"
	}
```

      In curly brackets, we will define which entity field corresponds to a certain data field in Doxis Smartbridge Service definition (Swagger). 

   * Example: mapping for sales order confirmation, where the Target Entity is SalesOrderConfirmationHeaderEntity
```json
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
```

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