<h1>Implementing custom Role Based Access Control (RBAC) roles</h1>

<h2>Introduction</h2>
<p>This article helps to create a custom Role Based Access Control (RBAC) to the user. This will help you to restrict the access to unauthorized users.</p>

<h2>Prerequisites</h2>
<p>To perform this demo user must have a valid Azure subscription and some basic knowledge on Azure Active Directory, Access control (IAM) and RBAC.</p>

<h2>Demo</h2>
<p>Log-in to Azure portal with your account using www.portal.azure.com. In Azure portal start a PowerShell session within the Cloud Shell. In the PowerShell panel run the following command to create a new resource group.</p>
	<p>New-AzResourceGroup -Name CodeSizzler_rg -Location "CentralUS"	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-006/01.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-006/02.jpg"/>
<p>After creating the resource group click on the upload icon to upload the template and parameter files. When it prompts upload azuredeploy09.json and azuredeploy09.parameters.json file to the Cloud Shell panel.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-006/03.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-006/04.jpg"/>
<p>After the uploading process completes run the following command to create a Virtual Machine hosting Ubuntu operating system.</p>
	<p>New-AzResourceGroupDeployment -ResourceGroupName CodeSizzler_rg -TemplateFile $home/azuredeploy09.json -TemplateParameterFile $home/azuredeploy09.parameters.json	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-006/05.jpg"/>
<p>Wait until the deployment gets complete. After the deployment gets completed close the PowerShell panel and navigate to the deployed resource group.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-006/06.jpg"/>
<p>From the overview panel of the resource group navigate to Access Control (IAM).</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-006/07.jpg"/>
<p>In the IAM panel click on Roles>Owner>Permissions.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-006/08.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-006/09.jpg"/>
<p>In the permissions panel click on Microsoft Compute.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-006/10.jpg"/>
<p>In the Microsoft Compute panel select Virtual Machines and when it prompts note that they include Deallocate Virtual Machine and Start Virtual Machine actions in the list of actions.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-006/11.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-006/12.jpg"/>
<p>Open the customRoleDefinition09.json file and review the content.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-006/13.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-006/14.jpg"/>
<p>After reviewing the content start the PowerShell session and click on the upload icon to upload the customRoleDefinition09.json file.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-006/15.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-006/16.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-006/17.jpg"/>
<p>After uploading the file run the following command to replace the subscription ID</p>
	<p>$subscription_id = (Get-AzContext).Subscription.id</p>
	<p>(Get-Content -Path $HOME/customRoleDefinition09.json) -Replace 'SUBSCRIPTION_ID', "$subscription_id" | Set-Content -Path $HOME/customRoleDefinition09.json	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-006/18.jpg"/>
<p>Run the folllowing command to create a new custom role defenition.</p>
	<p>New-AzRoleDefinition -InputFile $HOME/customRoleDefinition09.json	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-006/19.jpg"/>
<p>To verify that the custom role was created successfully run the following command and verify the output.</p>
	<p>Get-AzRoleDefinition -Name 'Virtual Machine Operator (Custom)'	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-006/20.jpg"/>
<p>To identify the Azure Active Directory DNS domain name run the following command.</p>
	<p>$domainName = ((Get-AzureAdTenantDetail).VerifiedDomains)[0].Name	</p>
<p>Run the following commands to create Azure Active Directory user.</p>
	<p>$passwordProfile = New-Object -TypeName Microsoft.Open.AzureAD.Model.PasswordProfile	  </p>
	<p>$passwordProfile.Password = 'demo@pass123'	</p>
	<p>$passwordProfile.ForceChangePasswordNextLogin = $false	</p>
	<p>New-AzureADUser -AccountEnabled $true -DisplayName 'demouser' -PasswordProfile $passwordProfile -MailNickName 'demouser' -UserPrincipalName "demouser@$domainName"	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-006/21.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-006/22.jpg"/>
<p>Close the Cloud Shell panel and open a private browser. In the private browser log in to Azure portal with the AD user that you created before in this exercise.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-006/23.jpg"/>
<p>In Azure portal navigate to the resource group and note that there are no resource groups available.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-006/24.jpg"/>
<p>From the resource group panel navigate to All resource panel.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-006/255.jpg"/>
<p>In the all resource panel note that the Virtual Machine that you created earlier in this demo is listed there.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-006/26.jpg"/>
<p>Navigate to the Virtual Machine. In the Virtual Machine overview panel try to restart the Virtual Machine and note the error message. Then try to stop the Virtual Machine and note that the task gets successfully completed.</p>








