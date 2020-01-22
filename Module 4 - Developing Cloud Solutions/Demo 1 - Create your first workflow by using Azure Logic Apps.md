<h1>Create your first workflow by using Azure Logic Apps</h1>

<h2>Introduction</h2>
<p>In this article you are going to learn about how to configure the workflows with Azure Logic app.</p>

<h2>Pre-requisites</h2>
<p>To perform this demo, you must have valid Azure subscription and some knowledge on Azure Logic app.</p>

<h2>Demo</h2>

<h2>Create your logic app:</h2>
<p>Log in the Azure portal with your account using??www.portal.azure.com?In the Azure portal click on create a new resource Search on a tab> Logic App.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-13/01.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-13/02.jpg"/>
<p>Create a logic App configure following settings:</p>
	<p>•Name: Codesizzlerlogic</p>
	<p>•Subscription: Select on azure subscription</p>
	<p>•Resource group: Create a new resource (codesizzler-01)</p>
	<p>•Location: Choose on azure region</p>
	<p>•Log Analytics: on</p>
<p>Finally Click on Create button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-13/03.jpg"/>
<p>In the azure portal select on Codesizzlerlogic app.>Development Tools>Logic app designer blade> Click on Blank Logic App blade.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-13/04.jpg"/>

<h2>Add the RSS trigger:</h2>
<p>1.In the Logic App Designer, under the search box, select All.</p>
<p>2.Select the When a feed item is published trigger.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-13/05.jpg"/>
<p>3.Provide this information for your trigger as shown and described here:</p>
	<p>•The RSS feed URL:  http://feeds.reuters.com/reuters/topNews</p>
	<p>•Interval: 1</p>
	<p>•Frequency: Minute</p>
<p>Finally click save button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-13/06.jpg"/>

<h2>Add the "send email" action:</h2>
<p>1.Under Choose an action and the search box, select All.</p>
<p>2.From the actions list, select the "send an email" action for the email service.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-13/07.jpg"/>
<p>3.Sign in your outlook account.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-13/08.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-13/09.jpg"/>
<p>Send an email following settings:</p>
	<p>•To: aasiff@codesizzler.info</p>
	<p>•Subject: Feed tittle</p>
	<p>•Body:</p>
	<p>•Tittle: Feed tittle</p>
	<p>•Date published: Feed published on</p>
	<p>•Link: Primary feed link</p>
<p>Finally Save logic app.</p>

<h2>Run your logic app:</h2>
<p>1.To manually start your logic app, on the designer toolbar bar, select Run.</p>
<p>2.Your logic app waits until the next interval before checking again. If you don't get any emails, check your junk email folder.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-13/10.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-13/11.jpg"/>
