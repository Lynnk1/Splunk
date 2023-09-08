
![test splunk 2](https://github.com/Lynnk1/images-in-readme/assets/89667260/677ac60f-7550-4338-8a41-c9124dae5006)
<h2>Description</h2>

<b>Splunk is a potent data analysis and monitoring tool that empowers organizations with actionable insights. Serving as a centralized repository and a universal forwarder for logs, Splunk excels in data ingestion, traffic monitoring, data visualization, and alert generation. Its versatility lends itself to a wide array of applications, including IT troubleshooting, robust data analysis, vigilant security monitoring, and effective compliance management. </b>
<br/>
<b> Here I will show you some mini projects of what Splunk can do!

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

<h2> Transaction Command </h2>
<b> You can use transaction command to locate events that match a specific criteria or investigate a correlation.</b>
<b> Compared to stats command, you can find user activity for logins, session duration length, network logs of interests, and more that helps aid investigations.</b>
