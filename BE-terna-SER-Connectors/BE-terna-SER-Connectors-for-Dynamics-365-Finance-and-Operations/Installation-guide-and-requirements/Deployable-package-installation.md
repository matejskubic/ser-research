Customers can update the software in their environments by applying different software deployable packages. For update process **all-in-one deployable packages are used,** which is a software deployable package that contains all the models and binaries that you currently have in an environment. Think of it as a single package that represents all the non-Microsoft software in an environment.

**Note:** This guide walks through the process of applying updates via Lifecycle Services (LCS). For other environments like **Local development environments** (Downloadable virtual hard disk [VHD]) or **Multi-box dev/test environments** in Microsoft Azure (Partner and trial projects) installation from the command line is required. More information about this topic can be found on [Microsoft's official sites.](https://learn.microsoft.com/en-us/dynamics365/fin-ops-core/dev-itpro/deployment/install-deployable-package)

When your local site configurations are ready to be deployed to your online environment, you must package and deploy them by using Microsoft Dynamics Lifecycle Services (LCS). So, first step is to upload required package to LCS:
1. Go to [https://lcs.dynamics.com](https://lcs.dynamics.com/Logon/Index) and log in.
2. Once in the main dashboard, select project for which you want to apply package
3. To upload the package, in the More tools (hamburger menu) section, select the **Asset Library tile.**
4. On the Asset library page, in the left pane, select **Software deployable package** menu
5. Select the plus sign (+).
6. In the Upload package file dialog box, enter a name and description for the package, and then select **Add a file.**
7. In the Upload file asset dialog box, select Browse, and browse to the location of the package zip file. Select the file, and then select Upload.
8. When the upload is completed, you're returned to the Upload package file dialog box. Select Confirm to process the upload.
9. After some time if the processing and validations were successfully completed, a check mark appears in the **Valid** column.


After the package is in the project asset library, follow these steps to update your environment:
1. Open the environment details page for the environment where you want to apply the package.
2. Select **Maintain > Apply updates** to apply an update.
3. Enter a **unique name** for the update. You will use this name to identify the update for which you want to promote the image (both the Microsoft binary and the customer AOT package) to the production environment.
4. Select the package to apply. Use the filter at the top to find your package. The list will include application and platform binary packages and application deployable packages that have passed validation from the asset library.
5. Select **Apply.** The status in the upper-right corner of the environment details page changes from **Queued** to **Servicing** and then to **Post-servicing**. When package application is completed, the status changes to **Deployed.**
6. After package application is completed, the environment history is updated. To view the environment history, select **History > Environment changes** on the environment details page.
7. You can also download the logs from the environment history page.
8. After the validations are completed, you can sign-off on the update from the environment history page by selecting either **Sign off** or **Sign off with issues.**

**Note: Package application causes system downtime.** All relevant services will be stopped, and you won't be able to use your environments while the package is being applied.

After you've successfully applied the update in the sandbox environment and are ready to move the update over to the production environment, follow these steps to mark an update as a release candidate:
1. Open the environment history page by selecting **History > Environment** changes on the environment details page.
2. Select the update to move over to the production environment.
3. In the details for the update, select **Mark as release candidate.** The Is **Release Candidate** option is set to **Yes.**

After you've marked an update as a release candidate, follow these steps to update your environment:
1. Open the environment details page for the production environment.
2. Select **Maintain > Update environment** to apply an update.
3. In the **Available sandboxes** list, select the source sandbox environment where the update was applied, validated, and marked as a release candidate.
4. In the grid, select the update to apply to the production environment. This grid shows only updates that have been marked as release candidates.
5. In the **Downtime start** field, select a date and time. The environment will be taken down for servicing at the specified time on the specified date. The **Downtime end** is calculated automatically based on the expected duration.
6. Select **Schedule.** LCS runs validations to make sure that the selected update is applicable to the environment. To prevent downgrade of the environment, the update isn't allowed if its application version is lower than the current environment version. If the update is **successfully** scheduled, an email notification is sent to all project stakeholders.
7. After the update is completed, the environment history is updated. To view the environment history, select **History > Environment** changes on the environment details page.
8. You can also download the logs from the environment history page.
9. After the validations are completed, you can sign-off on the update from the environment history page by selecting either **Sign off** or **Sign off with issues.**


More information about this topic can be found on Microsoft official sites:
* [All-in-one deployable packages](https://learn.microsoft.com/en-us/dynamics365/fin-ops-core/dev-itpro/dev-tools/aio-deployable-packages)
* [Update an environment](https://learn.microsoft.com/en-us/dynamics365/fin-ops-core/dev-itpro/deployment/updateenvironment-newinfrastructure)
* [Apply updates to cloud environments](https://learn.microsoft.com/en-us/dynamics365/fin-ops-core/dev-itpro/deployment/apply-deployable-package-system)
* [Manage third-party models and runtime packages by using source control](https://learn.microsoft.com/en-us/dynamics365/fin-ops-core/dev-itpro/dev-tools/manage-runtime-packages)


