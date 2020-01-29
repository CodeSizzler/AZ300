<h1>Creating automated, schedule-based, recurring workflows by using Azure Logic Apps</h1>

<h2>Introduction</h2>
<p>In this article you are going to learn about how creating Logic app and configuring workflows in Logic app using Azure portal.</p>

<h2>Pre-requisites</h2>
<p>To perform this demo, you must have valid Azure subscription and some knowledge on Azure Logic app.</p>

<h2>Create your logic app:</h2>
<p>1.Log in the Azure portal with your account using??www.portal.azure.com.?In the Azure portal click on?Create a new resource, under the Integration panel you fine the Logic App.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-14/01.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-14/02.jpg"/>
<p>2.Create logic app with the following configurations:</p>
	<p>•Name: Cloudapp</p>
	<p>•Subscription: Select on your subscription</p>
	<p>•Resource group: Create a new resource</p>
	<p>•Location: West Europe</p>
	<p>•Log Analytics: off</p>
<p>Finally click create button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-14/03.jpg"/>
<p>3.After the app is created, click Cloudlogic app. Then under Development Tools in the Logic Apps Designer and click the Blank Logic App template.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-14/04.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-14/05.jpg"/>
<h2>Add the Recurrence trigger:</h2>
<p>1.On the Logic App Designer, in the search box, enter "recurrence" as your filter. From the Triggers list, select the Recurrence trigger.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-14/06.jpg"/>
<p>2.Inside the trigger, change these properties.</p>
 	<p>•Interval: 1</p>
 	<p>•Frequency: Week</p>
 	<p>•Add new parameter list and select these properties to add to the trigger</p>
 	<p>•On these days</p>
 	<p>•At these hours</p>
 	<p>•At these minutes</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-14/07.jpg"/>
<p>3.Now set the values for the additional properties as shown and described here.</p>
	<p>•On these days: Monday, Tuesday, Wednesday, Thursday, Friday</p>
	<p>•At these hours: 7, 8, 9</p>
	<p>•At these minutes: 0, 15, 30, 45</p>
<p>Preview: This trigger fires every weekday, every 15 minutes, starting at 7:00 AM and ending at 9:45 AM. The Preview box shows the recurrence schedule.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-14/08.jpg"/>

<h2>Get the travel time for a route:</h2>
<p>1.In the Logic App Designer, under your trigger, select new step.</p>
<p>2.Under Choose an action, select Standard. In the search box, enter Bing maps.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-14/09.jpg"/>
<p>3.If you don't have a Bing Maps connection, you're asked to create a connection. Provide these connection details, and select Create.</p>
<p>4.Finally click save button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-14/10.jpg"/>
<p>5.Next step on inside the action, open the Add new parameter list, and select these properties to add to the action.</p>
	<p>•Optimize</p>
 	<p>•Distance unit</p>
 	<p>•Travel mode</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-14/11.jpg"/>
<p>6.Now set the values for the action's properties as shown and described here.</p>
	<p>•Optimize: Time with Traffic</p>
	<p>•Distance unit: Mile</p>
	<p>•Travel mode: Driving</p>
<p>Finally click save your logic app.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-14/12.jpg"/>

<h2>Create a variable to store travel time:</h2>
<p>1.Under the Get route action, select new step.</p>
<p>2.Under Choose an action, select Built-in. In the search box, enter variables, and select the Initialize variable action.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-14/13.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-14/14.jpg"/>
<p>3.Provide the details for your variable as described here:</p>
	<p>•	Name: Travel Time
	<p>•	Type: Integer
	<p>•	Value: Click inside the box so that the dynamic content list select Expression.
	<p>•	In the expression editor, enter this expression: div(,60)
	<p>•	In the dynamic content list, select Travel Duration Traffic.
<p>Save your logic app.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-14/15.jpg"/>

<h2>Compare the travel time with limit:</h2>
<p>1.Under the previous action, select new step.</p>
<p>2.Under Choose an action, select Built-in. In the search box, enter "condition" as your filter. From the actions list, select the Condition action.</p>
<p>3.In the condition, click inside the Choose a value box on the condition's left side.</p>
<p>4.From the dynamic content list that appears, under Variables, select the travelTime property.</p>
<p>5.In the middle comparison box, select the greater than operator.</p>
<p>6.In the Choose a value box on the condition's right side, enter this limit: 15</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-14/16.jpg"/>
<p>Finally click save your logic app.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-14/17.jpg"/>

<h2>Send email when limit exceeded:</h2>
<p>1.Click New Step choose an action, select Standard. In the search box, enter send email for select Office 365 Outlook.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-14/18.jpg"/>
<p>2.Logic Apps creates a connection to your email account.</p>
<p>3. Send an email enter the values:</p>
	<p>•To: Enter your email address.</p>
	<p>•Subject:</p>
	<p>•Enter the text Current travel time (minutes):</p>
	<p>•In the dynamic content list, under Variables, select see more.</p>
	<p>•After travelTime appears under Variables, select travelTime.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-14/19.jpg"/>
	<p>•Body:</p>
	<p>•Enter the text Add extra travel time (minutes): with a trailing space.</p>
	<p>•In the dynamic content list, select Expression.</p>
	<p>•In the expression editor, enter this expression so that you can calculate the number of minutes that exceed your limit: sub(,15)</p>
	<p>•Under Variables, select travelTime.</p>
	<p>•After the property resolves inside the expression, select OK.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-14/20.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az300-14/21.jpg"/>
<p>Save your logic app.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-14/22.jpg"/>

<h2>Run your logic app:</h2>
<p>1.To manually start your logic app, on the designer toolbar bar, select Run.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-14/23.jpg"/>
<p>2.If the current travel time exceeds your limit, you get an email with the current travel time and the number of minutes above your limit. Here is an example email that your logic app sends:</p>
<img src="https://codesizzlergit.blob.core.windows.net/az300-14/24.jpg"/>





