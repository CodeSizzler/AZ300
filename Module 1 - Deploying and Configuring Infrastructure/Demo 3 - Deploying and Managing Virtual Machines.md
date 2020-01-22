<h1>Deploying and Managing Virtual Machines</h1>

<h2>Demo</h2>
<h2>Installing and configuring HashiCorp Packer</h2>
<p>Log-in with your Azure account using www.portal.azure.com. Start a Bash session in Cloud Shell.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-007/01.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-007/02.jpg"/>
<p>Run the following commands in Bash to download and unzip the packer installation media.</p>
	<p>wget https://releases.hashicorp.com/packer/1.3.1/packer_1.3.1_linux_amd6	</p>
	<p>unzip packer_1.3.1_linux_amd64.zip	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-007/03.jpg"/>
<p>After installing and unzipping the installation package run the following command to create a resource group and service principal.</p>
	<p>RG=$(az group create --name DemoRG1 --location CentralUS) AAD_SP=$(az ad sp create-for-rbac)	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-007/04.jpg"/>
<p>After that upload template03.json in the Cloud Shell pane and run the following set of commands for configuring packer template.</p>
	<p>CLIENT_ID=$(echo $AAD_SP | jq .appId | tr -d '"')	</p>
	<p>CLIENT_SECRET=$(echo $AAD_SP | jq .password | tr -d '"')	</p>
	<p>TENANT_ID=$(echo $AAD_SP | jq .tenant | tr -d '"')	</p>
	<p>SUBSCRIPTION_ID=$(az account show --query id | tr -d '"')	</p>
	<p>LOCATION=$(echo $RG | jq .CentralUS | tr -d '"')	</p>
	<p>sed -i.bak1 's/"$CLIENT_ID"/"'"$CLIENT_ID"'"/' ~/template03.json	</p>
	<p>sed -i.bak2 's/"$CLIENT_SECRET"/"'"$CLIENT_SECRET"'"/' ~/template03.json
	<p>sed -i.bak3 's/"$TENANT_ID"/"'"$TENANT_ID"'"/' ~/template03.json	</p>
	<p>sed -i.bak4 's/"$SUBSCRIPTION_ID"/"'"$SUBSCRIPTION_ID"'"/' ~/template03.json		</p>
	<p>sed -i.bak5 's/"$LOCATION"/"'"$CentralUS"'"/' ~/template03.json	</p>
	<p>./packer build template03.json	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-007/05.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-007/06.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-007/07.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-007/08.jpg"/>
<p>After build completes run the following command to deploy an Azure Virtual Machine based on custom image.</p>
	<p>az vm create --resource-group DemoRG1 --name DemoVM --image demoimage --admin-username DemoUser --generate-ssh-keys	</p>
	<p>az vm open-port --resource-group DemoRG1 --name DemoVM --port 80	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-007/09.jpg"/>
<p>Wait until the deployment it will take some time. After the deployment run the following command to identify the IP address associated with the Virtual Machine.</p>
	<p>az network public-ip show --resource-group DemoRG1 --name DemoVMPublicIP --query ipAddress	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-007/10.jpg"/>
<p>Take a note on IP address and search for it in a Microsoft Windows Browser. Note that it shows the welcome page of nginx.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-007/11.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-007/12.jpg"/>













