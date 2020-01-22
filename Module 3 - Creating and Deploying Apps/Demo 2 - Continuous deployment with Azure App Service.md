<h1>Continuous deployment with Azure App Service</h2>

<h2>Introduction</h2>
<p>In this article you are going to learn about how to perform the continuous deployment with your Azure App Serving in Azure portal.</p>

<h2>Pre-requisites</h2>
<p>To perform this demo, you must have valid Azure subscription and some basic knowledge on Azure App service.</p>

<h2>Demo</h2>

<h2>Authorize Azure App Service:</h2>
<p>1.In the Azure portal search tab enter on App Services.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-11/01.jpg"/>
<p>2.Select the web app you want to deploy.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-11/02.jpg"/>
<p>3.On the web app page, select Deployment centre and on the deployment centre select GitHub finally click continue button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-11/03.jpg"/>
<p>4.On the Build provider page, select App Service build service, and then select Continue. Bitbucket always uses the App Service build service.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-11/04.jpg"/>
<p>5.On the Configure page</p>
	<p>•Organization: Codesizzler</p>
	<p>•Repository: Azure-WebApps</p>
	<p>•Branch: master</p>
<p>6.Finally Click on continue</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-11/05.jpg"/>
<p>7.After you configure the build provider, review the settings on the Summary page, and then select Finish.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-11/06.jpg"/>

<h2>Disable continuous deployment:</h2>
<p>To disable continuous deployment, select Disconnect at the top of your app's Deployment Center page.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-11/07.jpg"/>













