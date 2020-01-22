<h1>Create a Standard Load Balancer to VMs using the Azure portal</h1>

<h2>Introduction</h2>
<p>In this article you are going to learn about creating an Azure Load Balancer to balance the virtual Machines using Azure portal.</p>

<h2>Pre-requisites</h2>
<p>To perform this demo, you must have valid Azure subscription and some basic knowledge on Azure Load Balancer, Azure Virtual Machine.</p>

<h2>Create a Standard Load Balancer:</h2>
<p>Log in the Azure portal with your account using??www.portal.azure.com.?In the Azure portal click on?Create a new resource, under the Networking panel you can find the Load Balancer.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/01.jpg"/>
<p>Create a load balancer with the following configurations</p>
<p>Basic Tab</p>
<p>Project Details:</p>
	<p>•Subscription: Select on your subscription</p>
	<p>•Resource group: Create new ( Codesizzler-01 )</p>
<p>Instance Details:</p>
	<p>•Name: Codeloadbalance</p>
	<p>•Region: Choose on azure region</p>
	<p>•Type: Public</p>
	<p>•Sku: Standard</p>
	<p>•Public IP address: Create new</p>
	<p>•Public IP address name: cloud</p>
	<p>•Availability zone: zero-redundant</p>
<p>Finally click on Review + Create Button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/02.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/03.jpg"/>
<p>Once the deployment gets completed navigate to the created resource.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/04.jpg"/>

<h2>Create a backend address pool:</h2>
<p>Under Settings, select Backend pools, then select Add.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/05.jpg"/>
<p>Add backend pool with the following configurations</p>
	<p>•Name: mybackend pool.</p>
	<p>•Virtual Network: Search virtual network</p>
<p>Select Add Button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/06.jpg"/>

<h2>Create a health probe:</h2>
<p>Under settings select Health probes, then select Add.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/07.jpg"/>
<p>Add health probe with the following configurations</p>
	<p>•Name: cloud health</p>
	<p>•Protocol: HTTP</p>
	<p>•Port: 80</p>
	<p>•Path: 80</p>
	<p>•Interval: 15</p>
	<p>•Unhealthy threshold: 2</p>
<p>Select ok button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/08.jpg"/>

<h2>Create a Load Balancer rule:</h2>
<p>Under settings select Load balancing rules, then select Add.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/09.jpg"/>
<p>Add load balancer rule with the following configurations</p>
	<p>•Name: Myrule</p>
	<p>•Protocol: TCP</p>
	<p>•Port: 80</p>
	<p>•Backend port: 80</p>
	<p>•Backend pool: Codesizzlerpool</p>
	<p>•Health probe: cloudhealth</p>
<p>Select ok Button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/10.jpg"/>

<h2>Create a virtual network:</h2>
<p>In the Azure portal click on?Create a new resource, under the networking blade you can find the Virtual Network there.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/11.jpg"/>
<p>Create a Virtual network with following settings:</p>
	<p>•Name: AasiffVNET</p>
	<p>•Address space: 10.1.0.0/16</p>
	<p>•Subscription: Select on your subscription</p>
 	<p>•Resource group: exiting my resource> Codesizzler-01</p>
 	<p>•Location: West Europe</p>
 	<p>•Subnet name: cloud subnet</p>
 	<p>•Subnet Address range: 10.1.0.0/24</p>
<p>Finally select on create button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/12.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/13.jpg"/>

<h2>Create virtual machines:</h2>
<p>In the Azure portal Click on Create a new resource, under the  Compute blade you can Windows Server 2016 Datacenter.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/14.jpg"/>
<p>Create a Virtual Machine with following settings:</p>
<p>Basic Tab</p>
<p>Project Details:</p>
	<p>•Subscription: Select on your subscription</p>
	<p>•Resource group: Codesizzler-01</p>
<p>Instance Details:</p>
	<p>•Virtual Machine name: AasiffVM1</p>
	<p>•Region: Select on azure region ( West Europe )</p>
	<p>•Availability Options: Availability Zone</p>
	<p>•Availability Zones: 1</p>
<p>Administrator account:</p>
	<p>•User name: demouser</p>
	<p>•Password: *********</p>
	<p>•Confirm Password:*********</p>
<p>Click on Next: Disks button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/15.jpg"/>
<p>Click Next: Networking button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/16.jpg"/>
<p>Networking Tab</p>
<p>Network Interface:</p>
	<p>•Virtual Network: AasiffVNet</p>
	<p>•Subnet: cloudsubnet</p>
	<p>•Public IP> Create new</p>
	<p>•Name: AasiffVM-ip</p>
	<p>•SKU: Standard</p>
	<p>•Availability zone: zone-redundant</p>
<p>Click ok button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/17.jpg"/>
	<p>•Network Security group: Select Advanced</p>
	<p>•Name: AasiffVM1-nsg</p>
<p>Select ok button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/18.jpg"/>
<p>Load Balancing:</p>
	<p>•Place this virtual machine behind an existing load balancing solution: yes</p>
	<p>•Load balancing options: Azure load balancer</p>
	<p>•Select a load balancer: Codeloadbalance</p>
	<p>•Select a backend pool: Codesizzlerpool</p>
<p>Select on Next: Management button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/19.jpg"/>
<p>Management Tab</p>
<p>Monitoring:</p>
	<p>•Boot diagnostics: off</p>
<p>Select Review + create button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/20.jpg"/>
<p>Review the settings, and then select Create button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/21.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/22.jpg"/>
<p>Follow the steps 2 to 6 to create two additional VMs with the following values and all the other settings the same as AasiffVM1 to create another two Virtual Machines.</p>

<h2>Create NSG rule:</h2>
<p>Select all services in the left-hand menu, select all resources, and then from the resources list select Network Security Group.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/23.jpg"/>
<p>Under Settings, select Inbound security rules, and then select Add.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/24.jpg"/>
<p>Enter these values for the inbound security rule named myHTTPRule to allow for an inbound HTTP connections using port 80:</p>
	<p>•Source: Service Tag</p>
	<p>•Source service tag: Internet</p>
	<p>•Source port ranges: *</p>
	<p>•Destination: Any</p>
	<p>•Destination port ranges: 80</p>
	<p>•Protocol: TCP</p>
	<p>•Action: Allow</p>
	<p>•Priority: 100</p>
	<p>•Name: Myrule</p>
<p>Select Add button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/25.jpg"/>

<h2>Install IIS:</h2>
<p>Select all services in the left-hand menu, select all resources, and then from the resources list, select AasiffVM1.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/26.jpg"/>
<p>On the Overview page, select Connect to RDP into the VM.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/27.jpg"/>
<p>Download RDP File.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/28.jpg"/>
<p>Click Connect</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/29.jpg"/>
<p>Sign in the VM Account:</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/30.jpg"/>

<h2>Test the Load Balancer:</h2>
<p>•Find the public IP address for the Load Balancer on the Overview screen. Select all services in the left-hand menu, select all resources, and then select PublicIP.</p>
<p>•Copy the public IP address, and then paste it into the address bar of your browser. The default page of IIS Web server is displayed on the browser.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-009/31.jpg"/>











