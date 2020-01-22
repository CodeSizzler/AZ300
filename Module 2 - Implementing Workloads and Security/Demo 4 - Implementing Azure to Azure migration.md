<h1>Implementing Azure to Azure migration</h1>

<h2>AZ-300T02_Lab_Mod01_Implementing Azure to Azure migration.</h2>

<h2>Implement prerequisites for migration of Azure VMs by using Azure Site Recovery</h2>
<p>Login in to azure portal. In a upper portal click a cloud shell icon. And select a power shell window enter the following commands:</p>
	<p>New-AzResourceGroup -Name asma1RG -Location CentralUs	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-003/01.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-003/02.jpg"/>
<p>In the  upper power shell blade click a upload button and choose a \allfiles\AZ-300T02\Module_01\azuredeploy06.json into the home directory. And again choose a \allfiles\AZ-300T02\Module_01\azuredeploy06.parameters.json file.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-003/03.jpg"/>
<p>After the uploaded enter the following command:</p>
	<p>New-AzResourceGroupDeployment -ResourceGroupName asma1RG -TemplateFile azuredeploy06.json -TemplateParameterFile azuredeploy06.parameters.json	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-003/04.jpg"/>
<p>In a azure portal click a create a resource blade. Open the create a resource blade and type a Backup and Site Recovery (OMS) in a search box. And open the link click to a create button. And open the blade and create the newly recovery services vault. Type the following steps:</p>
	<p>•Name: asma02vault</p>
	<p>•Subscription: default</p>
	<p>•Resource group: asma02-RG</p>
	<p>•Location: default</p>
	<p>•Click a create button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-003/05.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-003/06.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-003/07.jpg"/>

<h2>Migrate an Azure VM between Azure regions by using Azure Site Recovery</h2>
<p>Select a newly deployed asma02vault recovery service vault blade under the resource group blade. On the Recovery Services vault blade, click the Replicate button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-003/08.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-003/09.jpg"/>
<p>And open the source blade and type the following steps:</p>
	<p>•Source: Azure</p>
	<p>•Source location: west Us</p>
	<p>•Azure virtual machine deployment model: Resource Manager</p>
	<p>•Source resource group: asma02-RG</p>
<p>And click a ok button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-003/10.jpg"/>
<p>And select a virtual machine blade and create a new VM.</p>
	<p>•Virtual machines: demovm,</p>
	<p>•Virtual network:asma1-vnet</p>
<p>And click an ok button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-003/11.jpg"/>
<p>And select a settings configuration blade a enter the following steps:</p>
	<p>•Target resource group: default</p>
	<p>•Target virtual network: default</p>
	<p>•Cache storage account: default</p>
	<p>•Replica managed disks: (new) 1 premium disk(s), 0 standard disk(s)</p>
	<p>•Target availability sets: Not Applicable</p>
	<p>•Replication policy: Create new</p>
	<p>•Name: 12-hour-retention-policy</p>
	<p>•Recovery point retention: 12 Hours</p>
	<p>•App consistent snapshot frequency: 6 Hours</p>
	<p>•Multi-VM consistency: No</p>
	<p>•And click a ok button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-003/12.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-003/13.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-003/14.jpg"/>






























