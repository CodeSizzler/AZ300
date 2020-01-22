<h1>Configuring RBAC for a resource using Azure portal</h1>

<h2>Introduction</h2>
<p>In this article you are going to learn about how to configure a role to your Azure resource in Azure portal.</p>

<h2>Pre-requisites</h2>
<p>To perform this demo, you must have valid Azure subscription and some basic knowledge on RBAC.</p>

<h2>Demo</h2>

<h2>Create a resource group:</h2>
<p>1.Log in the Azure portal with your account using??www.portal.azure.com?In the Azure portal click on the navigation list, click Resource groups.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-12/01.jpg"/>
<p>2.Click Add to open the Resource group blade.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-12/02.jpg"/>
<p>3.Create a resource group configure of following:</p>
<p>Basic Tab:</p>
	<p>•Subscription: Select on your azure subscription</p>
	<p>•Resource group: Create a new resource (Codesizzler-001)</p>
	<p>•Region: Choose on Azure region</p>
<p>Click on Review + create button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-12/03.jpg"/>
<p>Review + create Tab:</p>
<p>Click create button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-12/04.jpg"/>
<p>4.Click Refresh to refresh the list of resource groups and the new resource group appears in your resource groups list.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-12/05.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-12/06.jpg"/>

<h2>Grant access:</h2>
<p>1.In the list of Resource groups, click the new Codesizzler001 resource group.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-12/07.jpg"/>
<p>2.Click Access control (IAM) and click the Role assignments tab.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-12/08.jpg"/>
<p>Click Add >Add role assignment to open the Add role assignment tab.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-12/09.jpg"/>
<p>Add role assignment with the following settings:</p>
	<p>•Role: Virtual Machine Contributor</p>
	<p>•Assign access to: Azure AD user>group>or service principal</p>
	<p>•Select: Select on your name or email address</p>
<p>Finally click save button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-12/10.jpg"/>

<h2>Remove access:</h2>
<p>1.In the Role drop-down list, select Virtual Machine Contributor.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-12/11.jpg"/>
<p>2.In RBAC, to remove access, you remove a role assignment.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-12/12.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-12/13.jpg"/>


















