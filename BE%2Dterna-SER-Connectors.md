# Information about BE-terna Microsoft Dynamics 365 for Finance and Operations Connectors for SER Doxis
BE-terna D365FO SER Connectors are add-ons for Microsoft Dynamics 365 for Finance and Operations (D365FO) that enable users to merge their daily business process with the SER Doxis solution. There are two connectors available:
* **D365FO DIIA Connector**
Optimizes the invoice processing process between D365FO and SER Doxis by providing an API web service for invoice documents and master data synchronization such as Vendors, Cost center, Items, Categories etc..
* **D365FO Smartbridge Connector**
Enables automatic archiving of D365FO documents and data into SER Doxis Smartbridge providing a 360°view over processes and partners.

This document has three main parts:
* Installation guide and requirements
* D365FO DIIA Connector configuration, architecture and API structure 
* D365FO Smartbridge configuration, architecture

# Information about BE-terna Microsoft Dyamics 365 for Dataverse Connectors for SER Doxis
Please read the [Configuration Manual](https://dev.azure.com/BE-terna-SER/SER-Doxis/_git/SER-Doxis-Dataverse?path=/ConfigurationManual.docx)

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
