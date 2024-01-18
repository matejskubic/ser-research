# Information about BE-terna Microsoft Dyamics 365 for Dataverse Connectors for SER Doxis
Solution is allowing a configurable 1-way integration of entity metadata from Dataverse to Doxis solution document folders. Syncronization is triggered either manually or using the registered plugin steps as described in the manual. Azure infrastructure is used to transpose the documents according to the configuration to the Doxis endpoints.

Please read the [Configuration Manual](https://dev.azure.com/BE-terna-SER/SER-Doxis/_git/SER-Doxis-Dataverse?path=/ConfigurationManual.docx) for the architetecture overview and specific configuration options of the solution.

* Doxis is an extremely agile, scalable and secure platform for ECM, BPM and collabora-tion applications of all kinds. Through APIs and connectors, Doxis provides information, manages cross-system processes and connects to Dataverse / Dynamics CRM and other systems.
* Azure components
** Azure API Management is a reliable, secure and scalable way to publish, consume and manage API's running on Microsoft Azure platform
** Doxis CRM WebHooks API
*** Handles events from Dataverse / Dynamics 365 and tranforms them into Doxis API payload
**Azure App Configuration is an Azure service that allows users to store and manage configuration within the cloud 
	In this key-value storage, for each Doxis CRM WebHooks subscription, a set of configurations is stored
** Azure App Insights provides Application Performance Monitoring (also known as “APM”) features.
* Dataverse / Dynamics 365 organization
** Installed Doxis Connector Solution
** Installed Doxis Connector Solution Configuration (file that stores the configuration)

**Dataverse organizations** 

* Development
https://operations-be-ser-dev.crm4.dynamics.com (environment: be-ser-dev, Subscription: BE-terna (Part of Telefónica Tech), directory id: ff76d581-3569-4f50-9fe6-81d7f3166345)

**CRM Solutions**
* Doxis Connector Solution Configuration (This should be exported as unmanaged as it contains the initial solution configuration)
* Doxis Connector Solution (This should be exported as managed as it contains configuration application files)

**Azure Middleware components**
* Log Analytics workspace
* Application Insights
* Azure Monitor workspace
* BeTerna-SER-CRM-Config	App Configuration Service
* BeTerna-SER-CRM-WebHooks-NET6	Function App
* D365-document-managament-SER-Doxis-DEV-APIM	API Management service
* D365-SER-Doxis-DEV-KV	Key vault
* doxis.be-terna.net	DNS zone
* doxiswebhooksnet6	Storage account