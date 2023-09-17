
![test splunk 2](https://github.com/Lynnk1/images-in-readme/assets/89667260/677ac60f-7550-4338-8a41-c9124dae5006)
<h2>Description</h2>

<b>Splunk is a potent data analysis and monitoring tool that empowers organizations with actionable insights. Serving as a centralized repository and a universal forwarder for logs, Splunk excels in data ingestion, traffic monitoring, data visualization, and alert generation. Its versatility lends itself to a wide array of applications, including IT troubleshooting, robust data analysis, vigilant security monitoring, and effective compliance management. </b>
<br>

<b> Here I will show you what some projects that I learned from earning my Splunk Core Certified Power User certificate.

<h2>What you'll need </h2>

- <b>Splunk Enterprise.
<br/>Here is a free trial you can use for splunk enterprise https://www.splunk.com/en_us/products/splunk-enterprise.html
- <b>Practice_Data.zip, MOCK_DATA.csv, and cisco_ironport_web.log<br/>
<h2>Add-ons and adding data</h2>
- <b>Add-Ons:</b>
Splunk Add-on for Cisco WSA, Splunk Add-on for unix and Linux
<br/> <br/>
- <b>Input Data:</b> 
Your input phase will consist of host, source, and sourcetype.

| host      | source        | sourcetype |
| ----------|:-------------:| ------------:|
| web1      | access.log    | access_combined |
| web2      | cisco_ironport_web.log | cisco:wsa:squid |
| web3      | secure.log    | linux_secure  |
| web4 

<h2>Splunk use-cases walk-through:</h2>

<p align="center">
Launch the utility and login:</p>
<br/>

![login](https://github.com/Lynnk1/images-in-readme/assets/89667260/a6a43c0d-907b-4461-8fef-3a0b70a20728)

<h2> Finding events occuring from an ip address </h2>
<b> You can use transaction command to locate events that match a specific criteria or investigate a correlation.</b>
<b> Compared to stats command, you can find user activity for logins, session duration length, network logs of interests, and more that helps aid investigations.</b>
<br/> <br/>
Here we will use a simple transaction command looking for events with no pause between events greater than 3 seconds and using maxspan to show a maximum time of 5 minutes between the earliest and the latest events.
<br/> <br/>
 index=security 
<br/>
| transaction maxspan=5min maxpause=3s 
<br>
<br/>

![transaction](https://github.com/Lynnk1/Splunk/assets/89667260/b9e261f9-ae25-4f2c-b0e9-4a9a7ffe40fb) 

<br/>
We can go further by checking what actions have been taken by each diffrent ip sources.
<br/>
Note that we will search through the index of web this time. We will use the eval command to create a string called "duration" which will capture the time stamp. Then we will create a table for ip, duration, and action
<br/>
<br/>
index=web
<br/>
| transaction clientip maxspan=5min maxpause=3s
<br/>
| eval duration = tostring(duration, "duration")
<br/>
| table clientip, duration, action
<br>
<br/>

![transactiontwo](https://github.com/Lynnk1/images-in-readme/assets/89667260/c0818c87-6701-4c0c-ae6c-0eb0629241cc)
<br/>
<h2> Visualizing Data </h2>
<h>Data can be visualized in line charts, bar graphs, pie graphs, and more.</h>
<h>This helps data more comprehensible by transforming raw data to make it easier to understand patterns, behavior, and anomalies.</h>
<br> </br>
Let's look into the security index and identify failed login attempts.
<br> </br>
index=security eventtype=failed_login
</br>
| timechart count by user useother=f usenull=f limit=5
</br>

![failed login](https://github.com/Lynnk1/images-in-readme/assets/89667260/73403094-26a0-471b-a834-d229b3fbef97)
> We use the commands "useother=f", "usenull=f", and "limit=5" to filter out 'other' results and make it look less clustered.

> Be sure to select "Visualization" tab and select which format you would like your visualization to be displayed.
<br> </br>

Earlier we did a search to see what actions were taken by certain ip sources. We can also turn that into a bar graph to put on our dashboard.
<br> </br>
index=web
</br>
| where isnotnull(action)
</br>
| timechart count by action
</br>
![actions taken](https://github.com/Lynnk1/images-in-readme/assets/89667260/761a4155-4b6a-466a-a1aa-d047f7c7a593)
</br>
Actions are color coded in the bar graph and each bar represents the number of count.
> To show the data values on top of each bar, click on the format and turn on "Show Data Values"
<b></br>
<h2> Workflows </h2>
<b>The benefits of workflows is the ability to facilitate real time response. It creates an interaction between field events and web resources.</b>
<br>
<b>Below we will demonstrate the "GET" workflow action by using whois.domaintools.com as a web resource to look up any ip address of interest within our splunk.</b>
<br>
</br>

![whois](https://github.com/Lynnk1/images-in-readme/assets/89667260/1ee3dca9-a6e2-4736-9f1f-531f2bad09e6)
<br>
<br>
In Splunk, we will index our web in the search bar.
</br>
index=web
<br>
We can pick an event and go into details to use the IP address. Copy the IP address.
</br>
<br>
![eventlog](https://github.com/Lynnk1/images-in-readme/assets/89667260/214aeb7c-8a05-4a73-b55d-66714e2553c2)
<br>
Then, we will paste it into our whois.domaintools.com search bar. 
</br>
The results should display like this.
<br>
<br>
![domaintools](https://github.com/Lynnk1/images-in-readme/assets/89667260/2d0f87b3-89e5-4d53-a65a-69c3d90e4d71)
</br>
<br>
Now we don't have to always do this. Splunk allows to create workflows to make it interactable.
</br>
To do that, we'll need to head back to splunk and create the workflow in Settings > Fields > Add New next to Workflow Actions.
</br>
<br>
![whoissetting](https://github.com/Lynnk1/images-in-readme/assets/89667260/983dafa2-ea1f-4f1a-a14a-6861d98b1a5d)
</br>
<br>
Hit save and when you pull up the event actions in the fields, It will display a GET whois action that will redirect you to that url with the IP address.
</br>
<br>
![endresult](https://github.com/Lynnk1/images-in-readme/assets/89667260/eb2c3b9e-bbd7-4f92-984d-296c5a42d7bf)




