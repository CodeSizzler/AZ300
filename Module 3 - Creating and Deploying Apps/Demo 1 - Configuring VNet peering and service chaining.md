<h1>Configuring VNet peering and service chaining</h1>

<h2>AZ-300T02_Lab_Mod03_Configuring VNet peering and service chaining.md</h2>

<h2>Creating an Azure lab environment by using deployment templates</h2>
<p>Sign into azure portal. in the top of the azure portal click a cloud shell icon. And open the cloud shell select a bash window. And enter the following commands:</p>
	<p>az group create --resource-group asma01-RG --location central us</p>
	<p>az group create --resource-group asma02-RG --location central us</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/01.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/02.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/03.jpg"/>
<p>Bash pane, click the upload button. And select a template \allfiles\AZ-300T02\Module_03\azuredeploy0401.json. And again click the upload button and select a parameter file.  \allfiles\AZ-300T02\Module_03\azuredeploy04.parameters.json.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/04.jpg"/>
<p>And enter the following commands:</p>
	<p>az group deployment create --resource-group asma01-RG --template-file azuredeploy0401.json --parameters @azuredeploy04.parameters.json	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/05.jpg"/>
<p>And again click the upload button and select a \allfiles\AZ-300T02\ Module_03\ azuredeploy 0402 .json file. And run the following commands:</p>
	<p>az group deployment create --resource-group asma02-RG --template-file azuredeploy0402.json --parameters	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/06.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/07.jpg"/>

<h2>Configuring VNet peering</h2>
<p>In the azure portal open the virtual network blade and select a asma01-vnet. Open the asma01-vnet blade in a left corner selects a peerings blade. And click an Add button. And enter the following steps.</p>
	<p>•Name: asma01-vnet-to-asmaa02-vnet</p>
	<p>•Virtual network deployment model: Resource manager</p>
	<p>•Subscription: default</p>
	<p>•Virtual network: asma02-vnet</p>
	<p>•Allow virtual network access: Enabled</p>
	<p>•Finally click a ok button.</p>
	<p>•Allow forwarded traffic: disabled</p>
	<p>•Allow gateway transit: disabled</p>
	<p>•Use remote gateways: disabled</p>
Finally click a ok button.
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/08.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/09.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/10.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/11.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/12.jpg"/>
<p>In the azure portal click virtual networks. And select a asma02-vnet. Open the blade and click a peerings blade and select a add button. And enter the following steps:</p>
	<p>•Name: asma02-vnet-to-asma01-vnet</p>
	<p>•Virtual network deployment model: Resource manager</p>
	<p>•Subscription: default id</p>
	<p>•Virtual network: asma01-vnet</p>
	<p>•Allow virtual network access: Enabled</p>
	<p>•Allow forwarded traffic: disabled</p>
	<p>•Allow gateway transit: disabled</p>
	<p>•Use remote gateways: disabled</p>
	<p>•Finally click a ok button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/13.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/14.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/15.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/16.jpg"/>

<h2> Implementing routing</h2>
<p>Open the resource groups and select a asma01-nic2. And open the blade in a left corner click a ip configurations blade, and view the ip forwarding blade and click a enabled.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/17.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/18.jpg"/>
<p>In a azure portal type a route tables and open the blade click the create route table. Fill the following steps:</p>
	<p>•Name: asma02-rt1</p>
	<p>•Subscription: default id</p>
	<p>•Resource group: asma02-RG</p>
	<p>•Location: default id</p>
	<p>•BGP route propagation: Disabled</p>
	<p>•Finally click a create button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/19.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/20.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/21.jpg"/>
<p>Open the newly created the asma02-rt1 blade, in a left corner select a routes blade under the settings. And click a add button. And fill the following steps:</p>
	<p>•Route name: custom-route-to-asma01-vnet</p>
	<p>•Address prefix: 10.0.0.0/22</p>
	<p>•Next hop type: Virtual appliance</p>
	<p>•Next hop address: 10.0.1.4</p>
<p>In the Azure portal, associate the route table with the subnet-1 of the asma02-vnet.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/22.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/23.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/24.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/25.jpg"/>
<p>Open the resource groups’ blade and click a asma01-RG. And select a asma01-vm2. And open the blade, click a connect button. And select a download RDP file. And login the RDP windows.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/26.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/27.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/28.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/29.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/30.jpg"/>
<p>Open the remote desktop session. And open the server manager and install Remote Access server, start the Routing and Remote Access blade, and run Routing and Remote Access Server Setup Wizard and click LAN routing. start the Windows Firewall with Advanced Security, and click the File and Printer Sharing (Echo Request - ICMPv4-In) under the inbound rule.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/31.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/32.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/33.jpg"/>

<h2>Validating service chaining</h2>
<p>Open the resource groups and select a asma01-rg, and click a asma01-vm1 blade and select a connect button. And click a download a RDP file. And login the remote desktop session. And start the Windows Firewall with Advanced Security console and enable File and Printer Sharing (Echo Request - ICMPv4-In) under inbound rule.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/34.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/35.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/36.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/37.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/38.jpg"/>
<p>Open the resource group and select a asma02-rg, and click the asma02-vm1, and click a connect button. And click the download the RDP file. And login the RDP file. And open the powershell window and run the following commands:</p>
	<p>Test-NetConnection -ComputerName 10.0.0.4 -TraceRoute	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/39.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/40.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/41.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/42.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-004/43.jpg"/>

















