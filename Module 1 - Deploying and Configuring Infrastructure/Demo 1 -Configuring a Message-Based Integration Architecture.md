<h1>Configuring a Message-Based Integration Architecture</h1>

<h2>Introduction</h2>
<p>This article helps you to configure a message-based integration architecture. In this demo you are going to create a Storage account, Function app, Event Grid. Learn to upload a new blob to the Storage account container using the Azure Function app. Also learn how to generate the Azure Storage queues using Event Grid.</p>

<h2>Prerequisites</h2>
<p>To perform this demo user have a valid Azure subscription and some knowledge on Azure Storage account, Event Grid, Function apps and Bash.</p>

<h2>Demo</h2>
<p>Log-in to Azure portal with your account using www.portal.azure.com. In Azure portal start a Bash session within the Cloud Shell panel. If you are using the Cloud Shell for the first time you need to create a Storage account or-else you can start the Bash session normally.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-001/01.jpg"/>
<p>In the Bash panel run the following command to generate a pseudo-random string used as a prefix names for the resources that we are going to create in this lab.</p>
	<p>export PREFIX=$(echo `openssl rand 5 -base64 | cut -c1-7 | tr '[:upper:]' '[:lower:]' | tr -cd '[[:alnum:]]._-'`)	</p>
<p>After creating the pseudo ramdom string run the following command to set the location of the resources we are going to create in this lab.</p>
	<p>export LOCATION='CentralUS'	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-001/02.jpg"/>
<p>After setting the location of the resources run the following command to create a resource group which is going to contain all the resources we are going to create in this lab.</p>
	<p>export RESOURCE_GROUP_NAME='CodeSizzler_Rg'	</p>
	<p>az group create --name "${RESOURCE_GROUP_NAME}" --location $LOCATION		</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-001/03.jpg"/>
<p>Run the following commands to create a Storage account and a container in the Azure portal. This account will be used Azure functions.</p>
	<p>export STORAGE_ACCOUNT_NAME="workloadstorage${PREFIX}"	</p>
	<p>export CONTAINER_NAME="workcontainer"	</p>
	<p>export STORAGE_ACCOUNT=$(az storage account create --name "${STORAGE_ACCOUNT_NAME}" --kind "StorageV2" --location "${LOCATION}" --resource-group "${RESOURCE_GROUP_NAME}" --sku "Standard_LRS")	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-001/04.jpg"/>
<p>Run the following command to identify that the Storage account was created successfully. Note that the output turns true.</p>
	<p>az storage container create --name "${CONTAINER_NAME}" --account-name "${STORAGE_ACCOUNT_NAME}"	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-001/05.jpg"/>
<p>To store the connection string of the Storage account, create a variable by running the following command.</p>
	<p>export STORAGE_CONNECTION_STRING=$(az storage account show-connection-string --name "${STORAGE_ACCOUNT_NAME}" --resource-group "${RESOURCE_GROUP_NAME}" -o tsv)	</p>
<p>Run the following commands to create a Application Insight which is used to monitor the Azure Functions.</p>
	<p>export APPLICATION_INSIGHTS_NAME="codesizzlerappinsight${PREFIX}"	</p>
	<p>az resource create --name "${APPLICATION_INSIGHTS_NAME}" --location "${LOCATION}" --properties '{"Application_Type": "other", "ApplicationId": "function", "Flow_Type": "Redfield"}' --resource-group "${RESOURCE_GROUP_NAME}" --resource-type "Microsoft.Insights/components"	</p>
	<p>export APPINSIGHTS_KEY=$(az resource show --name "${APPLICATION_INSIGHTS_NAME}" --query "properties.InstrumentationKey" --resource-group "${RESOURCE_GROUP_NAME}" --resource-type "Microsoft.Insights/components" -o tsv)	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-001/06.jpg"/>
<p>To create an Azure Function in Azure portal run the following commands in the Bash panel.</p>
	<p>export FUNCTION_NAME="codesizzlerfunctionapp${PREFIX}"	</p>
	<p>az functionapp create --name "${FUNCTION_NAME}" --resource-group "${RESOURCE_GROUP_NAME}" --storage-account "${STORAGE_ACCOUNT_NAME}" --consumption-plan-location "${LOCATION}"	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-001/07.jpg"/>
<p>Run the following commands to configure the application settings if the Function app and to connect the Storage account with the Application Insight created earlier in this lab.	</p>
	<p>az functionapp config appsettings set --name "${FUNCTION_NAME}" --resource-group 	</p>
	<p>"${RESOURCE_GROUP_NAME}" --settings 	</p>
	<p>"APPINSIGHTS_INSTRUMENTATIONKEY=$APPINSIGHTS_KEY" FUNCTIONS_EXTENSION_VERSION=~2	</p>
	<p>az functionapp config appsettings set --name "${FUNCTION_NAME}" --resource-group 	</p>
	<p>"${RESOURCE_GROUP_NAME}" --settings	</p>
	<p>"STORAGE_CONNECTION_STRING=$STORAGE_CONNECTION_STRING" 	</p>
	<p>FUNCTIONS_EXTENSION_VERSION=~2	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-001/08.jpg"/>
<p>Close the Bash session and navigate to the created resource group in the Azure portal. In the resource group overview panel click the Function app created earlier in this lab. In the Function app blade click on +Function.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-001/09.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-001/10.jpg"/>
<p>When it prompts make sure that .Net entry appears and then click on Go.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-001/11.jpg"/>
<p>When it prompts select In Portal and click on go.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-001/12.jpg"/>
<p>In the create a function panel select More template and click on Finish and view template.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-001/13.jpg"/>
<p>In the choose template panel select Azure Blob Storage Trigger. When it prompts click on Install. Wait until the installation completes. After the installation process completes Click on Continue.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-001/14.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-001/15.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-001/16.jpg"/>
<p>In the new function panel configure the following and click on create.</p>
	<p>•Name: Give a valid name</p>
	<p>•Path: Storage account name/Container name</p>
	<p>•Storage account connection: STORAGE_CONNECTION_STRING</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-001/17.jpg"/>
<p>Navigate to the Function app panel and click on Storage trigger. In the storage trigger panel review the run.csx file.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-001/18.jpg"/>
<p>After that start the Bash session within the Cloud Shell panel. In the Bash panel run the following command to create a generate a pseudo-random string of characters which is going to be used as the prefix names for the resources going to be created.</p>
	<p>export PREFIX=$(echo `openssl rand 5 -base64 | cut -c1-7 | tr '[:upper:]' '[:lower:]' | tr -cd '[[:alnum:]]._-'`)
<img src="https://codesizzlergit.blob.core.windows.net/az300-001/19.jpg"/>
<p>After generating the pseudo string run the following commands to identify the Azure region of the existing resource group.</p>
	<p>export RESOURCE_GROUP_NAME_EXISTING='CodeSizzler_Rg'	</p>
	<p>export LOCATION=$(az group list --query "[?name == '${RESOURCE_GROUP_NAME_EXISTING}'].location" --output tsv)	</p>
	<p>export RESOURCE_GROUP_NAME='CodeSizzler_Rg'	</p>
	<p>az group create --name "${RESOURCE_GROUP_NAME}" --location $LOCATION		</p>
<p>After identifying the Azure region of the existing resource group run the following commands to create a Storage account and the container which is going to be used by the Event Grid that you are going to create in the next task.</p>
	<p>export STORAGE_ACCOUNT_NAME="eventstorage${PREFIX}"	</p>
	<p>export CONTAINER_NAME="eventworks"	</p>
	<p>export STORAGE_ACCOUNT=$(az storage account create --name "${STORAGE_ACCOUNT_NAME}" --kind "StorageV2" --location "${LOCATION}" --resource-group "${RESOURCE_GROUP_NAME}" --sku "Standard_LRS")	</p>
	<p>az storage container create --name "${CONTAINER_NAME}" --account-name "${STORAGE_ACCOUNT_NAME}"	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-001/20.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-001/21.jpg"/>
<p>Run the following command to create a variable which is going to store the ID property if the Storage account.</p>
	<p>export STORAGE_ACCOUNT_ID=$(az storage account show --name "${STORAGE_ACCOUNT_NAME}" --query "id" --resource-group "${RESOURCE_GROUP_NAME}" -o tsv)	</p>
<p>After creating the variable run the following commands to create a Storage account queue which is going to store the messages generated by the Event Grid.</p>
	<p>export QUEUE_NAME="storagequeue${PREFIX}"	</p>
	<p>az storage queue create --name "${QUEUE_NAME}" --account-name "${STORAGE_ACCOUNT_NAME}"	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-001/22.jpg"/>
<p>Run the following commands to create an Event Grid subscription which is going to generate the messages in Azure Storage.</p>
	<p>export QUEUE_SUBSCRIPTION_NAME="storagequeue${PREFIX}"	</p>

	<p>az eventgrid event-subscription create --name "${QUEUE_SUBSCRIPTION_NAME}" --included-event-types 'Microsoft.Storage.BlobCreated' --endpoint 	</p>
	<p>"${STORAGE_ACCOUNT_ID}/queueservices/default/queues/${QUEUE_NAME}" --endpoint-type "storagequeue" --source-resource-id "${STORAGE_ACCOUNT_ID}"	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-001/23.jpg"/>
<p>Run the following commands to upload a test blob to the Storage account that created earlier in this lab.</p>
	<p>export AZURE_STORAGE_ACCESS_KEY="$(az storage account keys list --account-name "${STORAGE_ACCOUNT_NAME}" --resource-group "${RESOURCE_GROUP_NAME}" --query "[0].value" --output tsv)"	</p>

	<p>export WORKITEM='workitem2.txt'	</p>

	<p>touch "${WORKITEM}"	</p>

	<p>az storage blob upload --file "${WORKITEM}" --container-name "${CONTAINER_NAME}" --name "${WORKITEM}" --auth-mode key --account-key "${AZURE_STORAGE_ACCESS_KEY}" --account-name "${STORAGE_ACCOUNT_NAME}"	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-001/24.jpg"/>
<p>After uploading the test blob to the Storage account navigate to the Storage account that you created in this lab. From the overview panel of the Storage account navigate to the queues blade and click on the entry which is representing the queue that you have created in this lab.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-001/25.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-001/26.jpg"/>


