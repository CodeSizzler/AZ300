<h1>Implementing Azure Load Balancer Standard</h1>

<h2>AZ-300T03_Lab_Mod03_Implementing Azure Load Balancer Standard.md</h2>
<h2>Implement inbound load balancing and NAT by using Azure Load Balancer Standard</h2>

<p>Sign into azure portal. Open the cloud shell pane and choose the BASH section. And enter the following commands:</p>
	<p>az group create --name asma0-RG --location centralus	</p>
<p>And open the upload button, and select the json file\allfiles\AZ-300T03 \Module_03\ azuredeploy0801. json and again open the upload button and select the parameter file \allfiles\AZ-300T03 \Module_03 \azuredeploy0801.parameters.json.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/01.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/02.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/03.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/04.jpg"/>
<p>az group deployment create --resource-group asma0-RG --template-file azuredeploy0801.json --parameters @azuredeploy0801.parameters.json	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/05.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/06.jpg"/>
<p>In a azure portal open the load balancer and click the create load balancer, and fill the following steps:</p>
	<p>•Subscription: default</p>
	<p>•Resource group: asma01-RG</p>
	<p>•Name: asma01</p>
	<p>•Region: central us</p>
	<p>•Type: Public</p>
	<p>•SKU: Standard</p>
	<p>•Public IP address: Create new named asma01-lb-pip01</p>
	<p>•Availability zone: Zone-redundant</p>
	<p>•Click to review+create</p>
	<p>•Click to create.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/07.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/08.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/09.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/10.jpg"/>
<p>Open the newly created asma01 load balancer blade, and open the blade click to backend pools, and select the add button.</p>
	<p>•Name: asma01-bepool</p>
	<p>•Virtual network: asma01-vnet (2 VM)</p>
	<p>•VIRTUAL MACHINE: asma01-vm0</p>
	<p>•IP ADDRESS: ipconfig1 (10.0.0.4) or ipconfig1 (10.0.0.5)</p>
	<p>•VIRTUAL MACHINE: asma01-vm1 </p>
	<p>•IP ADDRESS: ipconfig1 (10.0.0.5) or ipconfig1 (10.0.0.4)</p>
	<p>•Click to save button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/11.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/12.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/13.jpg"/>
<p>Back to asma01-backend pools, and click to health probes, and click to add button. Click a ok button.</p>
	<p>•Name: asma01-healthprobe</p>
	<p>•Protocol: TCP</p>
	<p>•Port: 80</p>
	<p>•Interval: 5</p>
	<p>•Unhealthy threshold: 2</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/14.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/15.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/16.jpg"/>
<p>Open the newly created asma01-healthprobs, and click to load balancing rules. And select a add button.</p>
	<p>•Name: asma01-lbrule01</p>
	<p>•IP Version: IPv4</p>
	<p>•Frontend IP address: 52.242.214.240( LoadBalancedFrontEnd)</p>
	<p>•Protocol: TCP</p>
	<p>•Port: 80</p>
	<p>•Backend port: 80</p>
	<p>•Backend pool: asma01-bepool (2 virtual machines</p>
	<p>•Health probe: asma01-healthprobe (TCP:80)</p>
	<p>•Session persistence: None</p>
	<p>•Idle timeout (minutes): 4</p>
	<p>•Floating IP (direct server return): Disabled</p>
	<p>•Click to ok button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/17.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/18.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/19.jpg"/>
<p>Open the asma01 blade and click to Inbound NAT rules. And open the add button. Fill the following steps:</p>
	<p>•Name: asma01-vm0-RDP</p>
	<p>•Frontend IP address: 52.242.214.240(LoadBalancedFrontEnd)</p>
	<p>•IP Version: IPv4</p>
	<p>•Service: RDP</p>
	<p>•Protocol: TCP</p>
	<p>•Port: 33890</p>
	<p>•Target virtual machine: asma01-vm0</p>
	<p>•Network IP configuration: ipconfig1 (10.0.0.4) or ipconfig1 (10.0.0.5)</p>
	<p>•Port mapping: Custom</p>
	<p>•Floating IP (direct server return): Disabled</p>
	<p>•Target port: 3389</p>
<p>And click to ok button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/20.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/21.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/22.jpg"/>
<p>Again back to asma01 blade annd click to add button, and fill the following steps:</p>
	<p>•Name: asma01-vm0-RDP</p>
	<p>•Frontend IP address: 52.242.214.240(LoadBalancedFrontEnd)</p>
	<p>•IP Version: IPv4</p>
	<p>•Service: RDP</p>
	<p>•Protocol: TCP</p>
	<p>•Port: 33890</p>
	<p>•Target virtual machine: asma01-vm0</p>
	<p>•Network IP configuration: ipconfig1 (10.0.0.5) or ipconfig1 (10.0.0.4)</p>
	<p>•Port mapping: Custom</p>
	<p>•Floating IP (direct server return): Disabled</p>
	<p>•Target port: 3389</p>
<p>And click to ok button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/23.jpg"/>
<p>Open the asma01 blade and copied the public ip address value. Open the new microsofft edge window and paste the ip value. And view the Internet Information Services Welcome page.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/24.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/25.jpg"/>
<p>Open the lap powershell window and run the following commands:</p>
	<p>mstsc /v:52.242.214.240:33890	</p>
<p>And open the remote desktop session and login the RDP. Open the local server manager and view the asma01-vm0</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/26.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/27.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/28.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/29.jpg"/>
<p> Open the local powershell window and type the following commands:</p>
	<p>mstsc /v:52.242.214.240:33891	</p>
<p>And login the RDP file. and open the local server manager annd view the asma01-vm1.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/30.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/31.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/32.jpg"/>
<p>Open the windows powershell and run the following commands, view the result.</p>
	<p>Invoke-RestMethod http://ipinfo.io/json	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/33.jpg"/>

<h2>Configure outbound SNAT traffic by using Azure Load Balancer Standard</h2>
<p>Open the  azure portal and click the cloudshell pane select the BASH section,and click the upload button and select a json file \allfiles\AZ-300T03\ Module_03\ azuredeploy0802Json.Agin open the upload pane and select the parameter file \allfiles\AZ-300T03\ Module_03\ azuredeploy0802.parameters.json.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/34.jpg"/>
<p>Run the following command</p>
	<p>az group deployment create --resource-group asma01-RG --template-file azuredeploy0802.json --parameters @azuredeploy0802.parameters.json	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/35.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/36.jpg"/>
<p>Run the following commands</p>
	<p>az network public-ip create --resource-group asma01-RG --name asma02-lb-pip01 --sku standard		</p>

	<p>LOCATION=$(az group show --name asma01-RG --query location --out tsv)	</p>

	<p>az network lb create --resource-group asma01-RG --name asma02-lb --sku standard --backend-pool-name asma02-bepool --frontend-ip-name loadBalancedFrontEndOutbound --location $LOCATION --public-ip-address asma02-lb-pip01	</p>

	<p>az network lb outbound-rule create --resource-group asma01-RG --lb-name asma02-lb --name outboundRuleasma02 --frontend-ip-configs loadBalancedFrontEndOutbound --protocol All --idle-timeout 15 --outbound-ports 10000 --address-pool asma02-bepool	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/37.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/38.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/39.jpg"/>
<p>In the azure portal click the laod balancer, and select the asma02-ib  blade, and click the backend pools, and click the asma02-bepool. And fill the following steps:</p>
	<p>•Virtual network: asma01-vnet (4 VM)</p>
	<p>•VIRTUAL MACHINE: asma02-vm0 IP ADDRESS: ipconfig1 (10.0.1.4) or ipconfig1 (10.0.1.5)</p>
	<p>•VIRTUAL MACHINE: asma02-vm1 IP ADDRESS: ipconfig1 (10.0.1.5) or ipconfig1 (10.0.1.4)</p>
	<p>•Click to save button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/40.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/41.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/42.jpg"/>
<p>Note the asma02-lb-pip01 public ip address value. And back to asma01-vm0 and click to connect button. and click the download RDP file. and open the windows powershell run the following command:</p>
	<p>mstsc /v:asma02-vm0	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/43.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/44.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/45.jpg"/>
<p>Login the RDP file. and open the local server manager and view the asma02-vm0. Back to windows powershell run the following commands and view the result.</p>
	<p>Invoke-RestMethod http://ipinfo.io/json 	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/46.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/47.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-002/48.jpg"/>









