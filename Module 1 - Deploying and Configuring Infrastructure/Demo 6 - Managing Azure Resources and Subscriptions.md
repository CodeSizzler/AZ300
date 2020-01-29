<h1>Managing Azure Resources and Subscriptions</h1>

<h2>Introduction</h2>
<p>In this article you are going to learn about how to manage your Azure subscriptions and Azure resources.</p>

<h2>Pre-requisites</h2>
<p>To perform this demo, you must have valid Azure subscription and some knowledge on Virtual Machien Scale Set, other Azure resources.</p>

<h2>Demo</h2>

<h2>1.Deploying Azure Virtual Machine Scale Sets</h2>
<p>Log-in with your Azure account using www.portal.azure.com. In Azure Portal start a PowerShell session and run the following command.</p>
	<p>Test-AzDnsAvailability -DomainNameLabel codedemo -Location 'CentralUS'</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-008/01.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-008/02.jpg"/>
<p>Note that the value of command returns true. If not use different values to the same command and run it.
<p>Use the quick start template to deploy auto scale demo app using https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-008/03.jpg"/>
<p>Click on Azure Deploy and log-in with an Azure account that has owner role on Azure subscription. It will navigate you to deploying Virtual Machine Scale Set.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-008/04.jpg"/>
<p>Deploy a Virtual Machine Scale Set with Python Bottle server & AutoScale with the following settings:</p>
	<p>•Subscription: Select a valid subscription</p>
	<p>•Resource group: Create a new resource group DemoRG</p>
	<p>•Location: Location used in PowerShell command</p>
	<p>•Vm Sku: Standard_D1_v2</p>
	<p>•Vmss Name: Custom label used in PowerShell command</p>
	<p>•Instance count: 1</p>
	<p>•Admin Username: DemoUser1</p>
	<p>•Admin Password: Codesizzler@</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-008/05.jpg"/>
<p>After the deployment completes navigate to the deployed scale set page and display the scaling page.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-008/06.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-008/07.jpg"/>
<p>Configure the scale set with following settings:</p>
	<p>•Scale out: increase instance count by 1 when average percentage of CPU > 60</p>
	<p>•Scale in: decrease instance count by 1 when average percentage of CPU < 30</p>
	<p>•Minimum number of instances: 1</p>
	<p>•Maximum number of instances: 3</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-008/08.jpg"/>

<h2>2.Implementing monitor and alert using Azure Monitor</h2>
<p>In Azure Portal navigate to the Monitoring-Metric blade and display the Average CPU Percentage. Review the CPU percentage for past few minutes.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-008/09.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-008/10.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-008/11.jpg"/>
<p>Navigate to alert page and click on create new rule. In the create rule panel navigate to resource panel and select the scale set resource.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-008/12.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-008/13.jpg"/>
<p>Navigate to Configure signal logic blade and select CPU percentage leave the other settings to default and change the aggregation period to 1. Leave the rest of settings to default.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-008/14.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-008/15.jpg"/>
<p>After setting the condition navigate to Add action group panel and add an action group with following settings:</p>
	<p>•Name: DemoActionGroup</p>
	<p>•Short name: DemoAction</p>
	<p>•Subscription: Select a valid subscription</p>
	<p>•Resource group: Accept the default one</p>
	<p>•Action name: DemoAction-email</p>
	<p>•Action type: Email/SMS/Push/Voice</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-008/16.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-008/17.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-008/18.jpg"/>
<p>Navigate to create rule panel and Set the alert name as DemoActionRule. Give any description and set the security to Sev3. Enable the rule and click on create alert rule.</p>
<p>It will take upto 10 mins to activate the alert rule.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-008/19.jpg"/>
<p>After creating the alert rule navigate to Monitor – Autoscale and click on Virtual Machine Scale Set deployed in the previous session.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-008/20.jpg"/>
<p>In the Autoscale setting panel click on notify and configure with following settings and save it.</p>
	<p>•Email administrators: Enable</p>
	<p>•Email co-administrators: Disable</p>
	<p>•Additional administrator emails(s): Add a valid email address</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-008/21.jpg"/>
<p>In Azure Portal navigate to the deployed Virtual Machine Scale Set panel and note the value public IP address of the Virtual Machine Scale Set.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-008/22.jpg"/>
<p>Open the browser and search for http://23.101.116.27:9000.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-008/23.jpg"/>
<p>When it prompts click on Start Work.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-008/24.jpg"/>
<p>Monitor the CPU utilization and navigate to instances panel of Virtual Machine Scale Set to identify the number of instances.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-008/25.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-008/26.jpg"/>
<p>After identifying the number of instances return to the browser and click on Stop working.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-008/27.jpg"/>
<p>Then navigate to Virtual Machine Scale Set panel and monitor the CPU usage.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-008/28.jpg"/>
