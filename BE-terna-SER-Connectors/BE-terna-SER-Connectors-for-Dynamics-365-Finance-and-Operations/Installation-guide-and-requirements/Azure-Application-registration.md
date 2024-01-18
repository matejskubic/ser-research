To use D365FO services, they must be registered with the Azure Active Directory (Azure AD) for cloud installation and AD FS for on-premises installation.

**To register a service with the Azure AD, follow these steps:**
1. Go to the **Azure Active Directory** tab of the Azure portal.
2. Select Properties and note the tenant ID in the Directory ID field. You will need the tenant ID later to retrieve an Azure AD authentication token.
3. On the Azure Active Directory tab, select **App registrations.**
4. Select **New application registration.**
5. Enter a name that identifies the external application that you're registering. For an application that will authenticate by using a shared secret, select **Web app / API.**
6. Select the new application and copy the application ID.
7. Select **Required permissions.**
8. Select Add.
9. Choose Select an API.
10. Select **Microsoft Dynamics ERP** (Microsoft.ERP).
11. Under Delegated permissions, you must select, at a minimum, the following options:
    * **Access Dynamics AX Custom Service**
    * **Access Dynamics AX data**
    * **Access Dynamics AX online as organization users**
12. Select Done.
13. Select Keys.
14. In the dialog box that appears, enter a description, and then set the Expires value to Never expires.
15. Select Save.

# Finance and Operations steps
When you've registered your service in Azure AD, you'll also need to register it in Finance and Operations apps by using the following steps:
1. In Finance and Operations apps, go to **System administration > Setup > Azure Active Directory applications.**
2. Select New.
3. In the **Client ID field,** enter the application ID that you registered in Azure AD.
4. In the Name field, enter a name for the application.
5. In the User ID field, select an appropriate service account user ID.
6. **Save** the record.



More information about this topic can be found on Microsoft official sites:
* [Microsoft D365FO Data management package REST API – Authorization](https://learn.microsoft.com/en-us/dynamics365/fin-ops-core/dev-itpro/data-entities/data-management-api#authorization)
* [Microsoft D365FO Authentication in on-premises environments](https://learn.microsoft.com/en-us/dynamics365/fin-ops-core/dev-itpro/deployment/authentication-onprem#ad-fs)
* [Client Id definition for cloud environment](https://learn.microsoft.com/en-us/power-apps/developer/data-platform/walkthrough-register-app-azure-active-directory)
* [Client Id definition for on-premises environment](https://learn.microsoft.com/en-us/dynamics365/fin-ops-core/dev-itpro/data-entities/services-home-page#authentication)
