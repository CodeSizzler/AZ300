<h1>Create an application gateway with a Web Application Firewall using the Azure portal</h1>

<h2>Introduction</h2>
<p>In this article you are going to learn about how to configure the Application Gateway with a Web Application Firewall in Azure portal.</p>

<h2>Pre-requisites</h2>
<p>To perform this demo, you must have valid Azure subscription and some basic knowledge on Azure Application Gateway.</p>

<h2>Demo</h2>

<h2>Create an application gateway:</h2>
<p>Log in the Azure portal with your account using??www.portal.azure.com. ?In the Azure portal click on?Create a new resource >Networking> Application gateway.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-15/01.jpg"/>
<p>Click on create an application gateway and configure the following settings:</p>
<p>Basics Tab:</p>
	<p>•Name: My Application Gateway</p>
	<p>•Tier: Standard</p>
	<p>•Instance Count: 2</p>
	<p>•SKU Size: Medium</p>
	<p>•Subscription: Select on your Subscription</p>
	<p>•Resource Group: Create a new resource ( AGresource )</p>
	<p>•Location: Choose Azure Region (South India)</p>
<p>Finally click OK button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-15/02.jpg"/>
<p>Settings Tab:</p>
<p>Under Virtual network >Choose a virtual network >Create new enter the following settings:</p>
	<p>•Name: AGVN</p>
	<p>•Address space: 10.2.0.0/16</p>
	<p>•Subnet name: myAGSubnet</p>
	<p>•Subnet address range: 10.2.0.0/24</p>
<p>Finally click OK button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-15/03.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-15/04.jpg"/>
<p>Summary Tab:</p>
<p>Click OK button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-15/05.jpg"/>
<p>In the Azure portal click on portal already create a resource> ( AGVN ) page under settings click Subnets blade.>click +Add Subnet.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-15/06.jpg"/>
<p>Add Subnet enter the following values:</p>
	<p>•Name: AGBsubnet</p>
	<p>•Address range: 10.0.0.0/24</p>
<p>On the click ok button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-15/07.jpg"/>

<h2>Create a virtual machine:</h2>
<p>In the Azure portal click on?Create a new resource> select compute> Select Windows Server 2016 Datacenter.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-15/08.jpg"/>
<p>Create a virtual Machine configuration of following settings:</p>
	<p>•Subscription: Select on your subscription</p>
	<p>•Resource group: Create a new resource ( AGresource )</p>
	<p>•Virtual Machine name: AGVM</p>
	<p>•Region: South India</p>
	<p>•Availability options: Availability Set</p>
	<p>•Availability Set: Create new> Myavast > finally select ok button.</p>
	<p>•On the Review + create tab, review the settings, correct any validation errors, and then select Create.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-15/09.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-15/10.jpg"/>

<h2>Install IIS for testing:</h2>
<p>Open Azure PowerShell. Select Cloud Shell from the top navigation bar of the Azure portal and then select PowerShell from the drop-down list.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-15/11.jpg"/>
<p>Run the following command to install IIS on the virtual machine:</p>
	<p>Set-AzVMExtension `	</p>
	 <p>-ResourceGroupName myResourceGroupAG `	</p>
	 <p>-ExtensionName IIS `	</p>
	 <p>-VMName myVM `	</p>
	 <p>-Publisher Microsoft.Compute `	</p>
	 <p>-ExtensionType CustomScriptExtension `	</p>
	 <p>-TypeHandlerVersion 1.4 `	</p>
	 <p>-SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `	</p>
 	<p>-Location EastUS	</p>
<p>Results:</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-15/12.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-15/13.jpg"/>
<p>Create a second virtual machine and install IIS by using the steps that you previously completed. Use myVM2 for the virtual machine name.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-15/14.jpg"/>
<p>Run the following command to install IIS on the virtual machine:</p>
	<p>Set-AzVMExtension `	</p>
	 <p>-ResourceGroupName myResourceGroupAG `	</p>
	 <p>-ExtensionName IIS `	</p>
	 <p>-VMName myVM2 `	</p>
	 <p>-Publisher Microsoft.Compute `	</p>
	 <p>-ExtensionType CustomScriptExtension `	</p>
	 <p>-TypeHandlerVersion 1.4 `	</p>
	 <p>-SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `	</p>
	<p>-Location EastUS	</p>
<p>Results:</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-15/15.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-15/16.jpg"/>

<h2>Add backend servers to backend pool:</h2>
<p>Select All resources, and then select myApplicationGateway and Backend pools from the left menu.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-15/17.jpg"/>
<p>Under Targets, select Virtual machine from the drop-down list and Virtual Machine and Network Interfaces select myVM and myVM2 virtual machines.</p>
<p>Finally Select Save.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-15/18.jpg"/>

<h2>Test the application gateway:</h2>
<p>Find the public IP address for the application gateway its Overview page. Copy the public IP address, and then paste it into the address bar of your browser.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-15/19.jpg"/>
<p>Check the response. A valid response verifies that the application gateway was successfully created and it can successfully connect with the backend.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-15/20.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-15/21.jpg"/>








