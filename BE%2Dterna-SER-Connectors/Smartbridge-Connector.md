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

For achieving an automatic document and data synchronisation the business event **SER_Doxis_SmartBridge_BusinessEvent**  must be activated for a selected legal entity (All about Business events and this type of integration in D365FO can be found on