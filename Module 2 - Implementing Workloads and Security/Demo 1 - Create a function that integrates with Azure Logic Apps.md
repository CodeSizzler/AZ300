<h1>Create a function that integrates with Azure Logic Apps</h1>

<h2>Introduction</h2>
<p>In this article you are going to learn about how to integrate your Function app with your Logic App.</p>

<h2>Pre-requisites</h2>
<p>To perform this demo, you must have valid Azure subscription and some basic knowledge on Azure Function app, Logic app, AI and Machine Learning.</p>

<h2>Demo</h2>

<h2>Create a Cognitive Services resource:</h2>
<p>1.Log in the Azure portal with your account using??www.portal.azure.com.?In the Azure portal click on?Create a new resource, under the AI+ Machine learning panel you find the Text Analytics.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/01.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/02.jpg"/>
<p>2.Create a Text Analytics with the following configurations:</p>
	<p>•Name: Codesizzlerservice</p>
	<p>•Subscription: Select on your subscription</p>
	<p>•Location: Use the location nearest (US) West US 2</p>
	<p>•Pricing tier: Select on F0</p>
	<p>•Resource group: Create a new resource ( Codesizzler-01 )</p>
<p>Click on Overview and copy the value of the Endpoint to a text editor. This value is used when creating a connection to the Cognitive Services API.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/03.jpg"/>
<p>3.Select the Notification icon in the portal and watch for the Deployment succeeded message.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/04.jpg"/>
<p>4.Click on Overview page and copy the value of the Endpoint. This value is used when creating a connection to the Cognitive Services API.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/05.jpg"/>
<p>5.Next step on click Keys, and then copy the value of Key 1. Use the key to connect the logic app to your Cognitive Services API.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/06.jpg"/>

<h2>Create the function app:</h2>
<p>1.In the Azure portal click on?Create a new resource, under the Compute panel you find the Function App.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/07.jpg"/>
<p>2.Create a Function App with following configurations:</p>
<p>Basic Tab</p>
<p>Project Details:</p>
	<p>•Subscription: Select on your subscription</p>
	<p>•Resource group: Select on a resource( Codesizzler-01 )</p>
<p>Instance Details:</p>
	<p>•Function App name: Codesizzlerfunctionapp</p>
	<p>•Publish: Select Code</p>
	<p>•Runtime stack: Select .NET Core</p>
	<p>•Region: Choose on azure region ( Central US )</p>
<p>Select the Next: Hosting > button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/08.jpg"/>
<p>3.Hosting Tab</p>
	<p>•Storage account name: codesizzlerstorage</p>
	<p>•Operating System: Windows</p>
	<p>•Plan type: Consumption plan</p>
<p>Select the Next: Monitoring > button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/09.jpg"/>
<p>4.Monitoring Tab</p>
	<p>•Application Insights: codesizzlerfunctionapp</p>
	<p>•Region: Central US</p>
<p>Select Review + Create button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/10.jpg"/>
<p>5.Select Create to provision and deploy the function app.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/11.jpg"/>
<p>6.Select the Notification icon in the portal and watch for the Deployment succeeded message.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/12.jpg"/>

<h2>Create an HTTP triggered function:</h2>
<p>1.Expand on the codesizzlerfunctionapp page. And Select the +New Functions.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/13.jpg"/>
<p>2.If this is the first function in your codesizzlerfunction app, select In-portal then click continue.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/14.jpg"/>
<p>3.Next, select Webhook + API and click Create.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/15.jpg"/>
<p>4.Next step on Replace the contents of the run.csx file with the following code, then click Save.</p>
	<p> #r "Newtonsoft.Json"	</p>

	<p>using System;	</p>
	<p>using System.Net;	</p>
	<p>using Microsoft.AspNetCore.Mvc;	</p>
	<p>using Microsoft.Extensions.Logging;	</p>
	<p>using Microsoft.Extensions.Primitives;	</p>
	<p>using Newtonsoft.Json;

	<p>public static async Task<IActionResult> Run(HttpRequest req, ILogger log)	</p>
	<p>{	</p>
  	  <p>string category = "GREEN";	</p>

   	 <p>string requestBody = await new StreamReader(req.Body).ReadToEndAsync();	</p>
   	 <p>log.LogInformation(string.Format("The sentiment score received is '{0}'.", requestBody));	</p>

   	 <p>double score = Convert.ToDouble(requestBody);	</p>
	<p>if(score < .3)	</p>
	 <p>{	</p>
        	<p>category = "RED";	</p>
   	 <p>}	</p>
    	<p>else if (score < .6)	</p>
    	 <p>{	</p>
        	<p>category = "YELLOW";	</p>
    	 <p>}	</p>
 	<p>return requestBody != null	</p>
        <p>? (ActionResult)new OkObjectResult(category)	</p>
        <p>: new BadRequestObjectResult("Please pass a value on the query string or in the request body");	</p>
	<p>}	</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/16.jpg"/>
<p>5.To test the function, click Test. Type a value of 0.2 for the Request body, and then click Run. A value of RED is returned in the body of the response.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/17.jpg"/>

<h2>Create a logic app:</h2>
<p>1.In the Azure portal click on?Create a new resource, under the Web panel you find the Logic App.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/18.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/19.jpg"/>
<p>2.Create a Logic App with following configurations:</p>
	<p>•Name: Cloudlogic</p>
	<p>•Subscription: Select on your subscription</p>
	<p>•Resource group: Use exisiting resource ( Codesizzler-01 )</p>
	<p>•Location: Use the location nearest ( West Central US )</p>
	<p>•Log Analytics: off.</p>
<p>3.Click on Create to logic app.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/20.jpg"/>
<p>4.After the app is created, click codesizzler logic app. Then under Development Tools in the Logic Apps Designer, and click the Blank Logic App template.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/21.jpg"/>

<h2>Connect to Twitter:</h2>
<p>1.In the designer, click the Twitter service, and click the When a new tweet is posted trigger. Sign in to your Twitter account and authorize Logic Apps to use your account.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/22.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/23.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/24.jpg"/>
<p>2.Next step on Use the Twitter trigger settings as specified in the table.</p>
	<p>•Search text: #azure</p>
	<p>•Interval: 15</p>
	<p>•Frequency: Minute</p>
<p>3.Then click Save to connect to your Twitter account.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/25.jpg"/>

<h2>Add sentiment detection:</h2>
<p>1.Click New Step, and then Add an action and next step Choose an action, type Text Analytics, and then click the Detect sentiment action.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/26.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/27.jpg"/>
<p>2.Text Analytics with the following configurations:</p>
	<p>•Connection name: MyCognitiveServicesConnection.</p>
	<p>•Account key: Paste the key for your Cognitive Services API.</p>
	<p>•Site URL:  Paste the Cognitive Services endpoint.</p>
<p>Click on Create button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/28.jpg"/>
<p>3.Then click on New Step and enter Tweet Text: Select Tweet Text.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/29.jpg"/>


<h2>Connect sentiment output to your function:</h2>
<p>1.Click New step > Choose an action, Azure Functions and click Choose an Azure function.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/30.jpg"/>
<p>2.Select the codesizzlerfunctionapp created earlier.</p>
<<img src="https://codesizzlergit.blob.core.windows.net/az300-10/31.jpg"/>
<p>3.Select the codesizzlerfunctionapp created for this tutorial. ( HttpTrigger1 )</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/32.jpg"/>
<p>4.In Request Body click Score and then click save button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/33.jpg"/>


<h2>Add email notifications:</h2>
<p>1.In the Logic Apps Designer, click New step > Add a condition.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/34.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/35.jpg"/>
<p>2.Click Choose a value Click then choose Body.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/36.jpg"/>
<p>3.In IF TRUE, click Add an action, search for outlook.com click Send an email, and sign in to your Outlook.com account.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/37.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/38.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/39.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/40.jpg"/>
<p>Note: If you don’t have an Outlook.com account, you can choose another connector, such as Gmail or Office 365 Outlook.</p>
<p>4.The Send an email action, use the email settings as specified in the table.</p>
	<p>•To: Enter your email address</p>
	<p>•Subject: Tweeted by</p>
	<p>•Body: Tweet text, Location</p>
<p>Finally Click Save.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/41.jpg"/>

<h2>Test the workflow:</h2>
<p>1.In the Logic App Designer, click Run to start the app.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/42.jpg"/>
<p>2.In the left column, click Overview to see the status of the logic app.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-10/43.jpg"/>










