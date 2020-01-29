<h1>Implementing user-assigned managed identities for Azure resources</h1>

<h2>Introduction</h2>
<p>In this article you are going to learn about how to implement managed identities for your Azure resources using Azure portal.</p>

<h2>Pre-requisites</h2>
<p>To perform this demo, you must have valid Azure account and some basic knowledge on Azure Managed Identities.</p>

<h2>Demo</h2>
<p>Log-in with Azure Portal using www.portal.azure.com. Start a Bash session in Cloud Shell panel. Upload the template files azuredeploy05.json and azuredeploy05.parameters.json in the Cloud Shell panel. After uploading the template files run the following commands to create a resource group and Virtual Machines. By running these commands, you are going to deploy a resource group and two Virtual Machines.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-005/01.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-005/02.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-005/03.jpg"/>

	<p>az group create --resource-group DemoRg1 --location CentralUS
	<p>az group deployment create --resource-group DemoRg1 --template-file azuredeploy05.json --parameters @azuredeploy05.parameters.json	</p>
<p>Wait for the deployment it may take upto five minutes. After the deployment completes run the following commands to create a user assigned managed identity to the Azure Virtual Machine.</p>
	<p>az identity create --resource-group DemoRg1 --name Demo-mi	</p>
	<p>az vm identity assign --resource-group DemoRg1 --name demovm --identities demo-mi	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-005/04.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-005/05.jpg"/>
<p>After that run the following command to create a new resource group.</p>
	<p>az group create --resource-group DemoRg2 --location CentralUS	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-005/06.jpg"/>
<p>After the command run completes navigate to DemoRg2 resource group and view Access control (IAM) panel. Assign owner role for newly created managed identity.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-005/07.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-005/08.jpg"/>
<p>Navigate to demovm panel and connect to the Virtual Machine using the credentials that you provided while creating the Virtual Machine.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-005/09.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-005/10.jpg"/>
<p>While entering the Virtual Machine it will open the Command prompt. In the command prompt type PowerShell and press enter. Then run the following commands.</p>
	<p>Install-Module -Name PowerShellGet -Force	</p>
	<p>Install-Module -Name Az -AllowClobber	</p>
<p>After the command runs exit the PowerShell session by typing Exit and restart the PowerShell session by typing PowerShell. Then run the following commands.</p>
	<p>Install-Module -Name PowerShellGet -AllowPrerelease	</p>
	<p>Install-Module -Name Az.ManagedServiceIdentity -AllowPrerelease	</p>
<p>Then run the following commands to validate the managed identity from the Virtual Machine.</p>
	<p>Add-AzAccount -Identity	</p>
	<p>(Get-AzVM -ResourceGroupName DemoRg1 -Name demovm).Identity	</p>
<p>Note that you will get an error while running the above command due to the security contest. Navigate to DemoRg1 and view the Access control panel. Assign reader role for user-assigned managed identity of DemoRg1-mi.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-005/11.jpg"/>
<p>After assigning the reader role navigate to the Virtual Machine and run the command.</p>
	<p>(Get-AzVM -ResourceGroupName DemoRg1 -Name demovm).Identity	</p>
<p>Note that this time you will get the identity of the resource group. Now run the following command to create an IP address of the resource group.</p>
	<p>$location = (Get-AzResourceGroup -Name DemoRg2).Location	</p>
	<p>New-AzPublicIpAddress -Name demo-pip -ResourceGroupName DemoRg2 -AllocationMethod Dynamic -Location $location	</p>

