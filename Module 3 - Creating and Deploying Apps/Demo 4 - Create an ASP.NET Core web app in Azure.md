<h1>Create an ASP.NET Core web app in Azure</h1>

<h2>Introduction</h2>
<p>In this article you are going to learn about how to deploy a Web app using Visual Studio.</p>

<h2>Pre-requisites</h2>
<p>To perform this demo, you must have valid Azure subscription and some basic knowledge on Web app, Visual Studio.</p>

<h2>Demo</h2>

<h2>Create an ASP.NET Core web app:</h2>
<p>1.Open Visual Studio and then select Create a new project.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-16/01.jpg"/>
<p>2.Choose on ASP.NET Core Web Application for C#, then select Next button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-16/02.jpg"/>
<p>3.In the Configure your new project following values:</p>
	<p>•Project Name: myfirstWebApp</p>
	<p>•Then select Create button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-16/03.jpg"/>
<p>4.Next step on choose the Web Application template. Make sure authentication is set to No Authentication and select create button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-16/04.jpg"/>
<p>5.You can deploy any type of ASP.NET Core web app to Azure.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-16/05.jpg"/>

<h2>Publish your web app:</h2>
<p>1.In Solution Explorer, right-click the myFirstAzureWebApp project and select Publish.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-16/06.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-16/07.jpg"/>
<p>2.Choose on App Service and create new then select create profile button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-16/08.jpg"/>
<p>3.Sign in for the Azure portal create a resource group.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-16/09.jpg"/>
<p>4.For the Hosting Plan, select New.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-16/10.jpg"/>
<p>5.In the Configure Hosting Plan, enter the values from the following table, and then select OK.</p>
	<p>•Hosting plan: myFirstAzureWebApp20200116054248plan</p>
	<p>•Location: West Europe</p>
	<p>•Size: Free</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-16/11.jpg"/>
<p>6.In Name, enter a unique app name select Create to start creating the Azure resources.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-16/12.jpg"/>

<h2>Update the app and redeploy:</h2>
<p>1.In Solution Explorer, under your project, open Pages > Index.cshtml</p>
<p>2.Replace the two <div> tags with the following code:</p>
	<p><div class="jumbotron">	</p>
	    <p><h1>ASP.NET in Azure!</h1>	</p>
	    <p><p class="lead">This is a simple app that we’ve built that demonstrates how to deploy a .NET app to Azure App Service.</p>	</p>
	<p></div>	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-16/13.jpg"/>
<p>3.To deploy to Azure, right-click the myFirstAzureWebApp project in Solution Explorer and select Publish.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-16/14.jpg"/>
<p>4.When publishing completes, Visual Studio launches a browser with the URL of the web app.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-16/15.jpg"/>















