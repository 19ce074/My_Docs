# Host a full stack website in Azure.
## Service used: 
+ **Azure app service** to host backend.
+ **Azure blob** for static-website to host frontend.
+ **Azure database** for Mysql server to host database.
 
## 1) Create a Resource group:

Sure! Here are the steps to create a resource group in Microsoft Azure in Markdown format:

1. Sign in to the Azure portal at [https://portal.azure.com](https://portal.azure.com) using your Azure account credentials.

2. Once you're signed in, click on the "Resource groups" option in the left-hand navigation menu.

3. In the "Resource groups" blade, click on the "+ Add" button to create a new resource group.

4. In the "Basics" tab of the "Create a resource group" page, fill in the following details:
   - **Subscription:** Select the Azure subscription you want to use.
   - **Resource group:** Enter a unique name for your resource group. The name can contain letters, numbers, periods, underscores, and hyphens.
   - **Region:** Select the Azure region where you want your resource group to be located.

5. Click on the "Next: Tags" button to proceed to the next tab, or you can skip this step if you don't want to add any tags.

6. In the "Tags" tab, you can add tags to your resource group if needed. Tags are name-value pairs that help you organize and categorize resources.

7. Click on the "Next: Review + Create" button to proceed to the next tab.

8. In the "Review + Create" tab, review the details you provided for the resource group. If everything looks correct, click on the "Create" button to create the resource group.

9. Azure will now validate the provided information and create the resource group. This process may take a few moments.

10. Once the resource group is created successfully, you will see a notification indicating that the deployment is complete. You can then click on the "Go to resource group" button to navigate to the newly created resource group.

## 2) Create Azure App service 





Sure! Here are the steps to create an Azure App Service in Markdown syntax:

1. **Sign in to Azure Portal**: Open a web browser and navigate to the [Azure Portal](https://portal.azure.com/). Sign in with your Azure account credentials.

2. **Create a new resource**: Once you are signed in, click on the "Create a resource" button in the Azure Portal.

3. **Search for App Service**: In the Azure Marketplace, search for "App Service" and select the "App Service" option from the results.

4. **Configure the App Service**: In the App Service creation page, provide the following details:

   - **Subscription**: Select the Azure subscription you want to use for the App Service.
   - **Resource Group**: Choose an existing resource group or create a new one to organize your resources.
   - **Name**: Enter a unique name for your App Service.
   - **Publish**: Select the appropriate option based on your application requirements.
   - **Runtime Stack**: Choose the desired runtime stack for your application (e.g., Node.js, .NET, Python).
   - **Operating System**: Select the operating system (Windows or Linux) for your App Service.
   - **Region**: Choose the Azure region where you want your App Service to be hosted.
   - **App Service Plan**: Select an existing plan or create a new one to specify the computing resources for your App Service.

   Adjust the settings according to your requirements.

5. **Create the App Service**: Once you have configured the necessary settings, click on the "Review + Create" button to review your configuration.

6. **Review and create**: Review the summary of your App Service configuration. Ensure that all the details are correct, and click on the "Create" button to create the App Service.

7. **Wait for deployment**: Azure will start deploying your App Service. Wait for the deployment to complete. You can monitor the deployment progress in the Azure Portal.

8. **Access your App Service**: Once the deployment is complete, you can access your App Service using the assigned URL or custom domain (if configured). You can find the URL under the "Overview" section of your App Service in the Azure Portal.

## 3) Create blob to host frontend

To host a static website in Azure Blob Storage using the Static Website feature, you can follow these steps:

1. **Create an Azure Storage Account**: If you don't have one already, create an Azure Storage Account by navigating to the Azure portal and selecting "Create a resource." Search for "Storage Account" and follow the instructions to create a new storage account.

2. **Create a Blob Container**: Within the created storage account, create a new Blob Container to store your static website files. Go to the Storage Account, navigate to "Containers," and select "Create Container." Provide a unique name and choose the appropriate access level (e.g., Blob, Private, or Public).

3. **Upload Website Files**: Upload your static website files to the Blob Container. You can use Azure Storage Explorer, Azure CLI, or Azure portal's web interface to upload the files. Ensure that you include an `index.html` file as the main entry point for your website. Note that the file structure should be preserved

4. **Configure Blob Storage for Static Website Hosting**: In the Azure portal, navigate to the Blob Container you created in Step 2. Select "Static website" from the sidebar and enable the feature. Provide the name of your default document (e.g., "index.html") and optionally, add a custom error document.

5. **Set Container Access Level**: Configure the access level of the Blob Container to allow public access. Select the "Access control (IAM)" option from the sidebar, choose "Add," and provide the appropriate permissions for anonymous access to your website files.

6. **Access the Static Website**: Once the static website hosting is enabled and container access is configured, you can access your website using the provided endpoint. It will be in the format `https://<storageaccountname>.<blobendpoint>/<containername>`.



