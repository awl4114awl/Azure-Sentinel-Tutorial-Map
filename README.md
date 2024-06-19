<p align="center">
<img src="https://i.imgur.com/SqeHdrU.png" height="20%" width="20%" alt="Azure Sentinel Tutorial"/>
<h1>Microsoft Azure Sentinel Map with Live Cyber Attacks</h1>

In this tutorial I'm going to use Microsoft Azure to construct a honeypot VM. I start by creating an Azure subscription and a virtual machine. I then disable any Windows firewalls to expose the VM to the internet, thus luring attackers. Then, I create a Log Analytics Workspace in Azure and connect it to the VM for log ingestion. After that, I use a custom PowerShell script to look up the attackers Geolocation information. Once that's over I create a custom log with this data, set up Azure Sentinel, and create a map using Sentinel to visualize attacker data and their geographic origins.
<br />

<h2>Languages and Utilities Used</h2>

- <b>PowerShell: Extract RDP failed logon logs from Windows Event Viewer</b> 
- <b>ipgeolocation.io: IP Address to Geolocation API</b>
- <b>Event Viewer</b>
- <b>Microsoft Azure</b>

<h2>Environments Used </h2>

- <b>Windows 10 VM</b> (22H2)
- <b>Windows 10 </b> (22H2)

<h2>Program walk-through:</h2>


    set up azure account:
<p align="center">
<img src="https://i.imgur.com/sDtn5Ea.jpeg" height="80%" width="80%" alt="Azure Sentinel Tutorial"/>
<br />
<br />
 
    create virtual machine (honeypot): 
<p align="center">
 <img src="https://i.imgur.com/NxDZc38.jpeg" height="80%" width="80%" alt="Azure Sentinel Tutorial"/>
<img src="https://i.imgur.com/LJmZO0C.jpeg" height="80%" width="80%" alt="Azure Sentinel Tutorial"/>
<br />
<br />
 
    add my own inbound security rule  in a resourced network security group:
<p align="center">
<img src="https://i.imgur.com/o5yE591.jpeg" height="80%" width="80%" alt="Azure Sentinel Tutorial"/>
<br />
<br />
 
    create a log analytics workspace:
<p align="center">
<img src="https://i.imgur.com/V3hjP75.jpeg" height="80%" width="80%" alt="Azure Sentinel Tutorial"/>
<br />
<br />
 
    turn sql servers off and change data collection settings to 'All Events':
<p align="center">
<img src="https://i.imgur.com/Se1p7zv.jpeg" height="80%" width="80%" alt="Azure Sentinel Tutorial"/>
<img src="https://i.imgur.com/cVv66dr.jpeg" height="80%" width="80%" alt="Azure Sentinel Tutorial"/>
<br />
<br />
 
    connect honeypot-vm to log analytics workspace: 
<p align="center">
<img src="https://i.imgur.com/6rnMeTQ.jpeg" height="80%" width="80%" alt="Azure Sentinel Tutorial"/>
<br />
<br />
 
    add microsoft sentinel to log analytics workspace: 
<p align="center">
<img src="https://i.imgur.com/4Q8hkf2.jpeg" height="80%" width="80%" alt="Azure Sentinel Tutorial"/>
<br />
<br />

    log in to vm with remote desktop:
<p align="center">
<img src="https://i.imgur.com/Tb4wLLV.jpeg" height="80%" width="80%" alt="Azure Sentinel Tutorial"/>
<img src="https://i.imgur.com/8G4zKMa.jpeg" height="80%" width="80%" alt="Azure Sentinel Tutorial"/>
<br />
<br />
 
    observe Event Viewer logs in vm:
<p align="center">
<img src="https://i.imgur.com/PKWMnaJ.jpeg" height="80%" width="80%" alt="Azure Sentinel Tutorial"/>
<br />
<br />
 
    turn firewall off on VM:
<p align="center">
<img src="https://i.imgur.com/nLqvtd5.jpeg" height="80%" width="80%" alt="Azure Sentinel Tutorial"/>
<br />
<br />
 
    download powershell script:
<p align="center">
<img src="https://i.imgur.com/O2sang4.jpeg" height="80%" width="80%" alt="Azure Sentinel Tutorial"/>
<br />
<br />
 
    get geolocation.io api key:
<p align="center">
<img src="https://i.imgur.com/7bJDbC1.jpeg" height="80%" width="80%" alt="Azure Sentinel Tutorial"/>
<br />
<br />
 
    run script to get data from attackers:
    the script runs in perpetuality looks through the event logs and grabs all the events of people who failed to login grabs ip address and gets geo data for them and then creates a log file. full script used --> https://shorturl.at/8fP31
<p align="center">
<img src="https://i.imgur.com/H8QwMva.jpeg" height="80%" width="80%" alt="Azure Sentinel Tutorial"/>
<br />
<br />

    create custom log in log analytics workspace to bring in our custom log: 
<p align="center">
<img src="https://i.imgur.com/qGMB4OK.jpeg" height="80%" width="80%" alt="Azure Sentinel Tutorial"/>
<img src="https://i.imgur.com/XntCFWQ.jpeg" height="80%" width="80%" alt="Azure Sentinel Tutorial"/>
<br />
<br />
 
    create custom fields/extract fields from raw custom log data:
<p align="center">
<img src="https://i.imgur.com/Zy4XWcc.jpeg" height="80%" width="80%" alt="Azure Sentinel Tutorial"/>
<br />
<br />
 
    setup map in sentinel with latitude and longitude (or country), also create a new workbook in Microsoft Sentinel and add a new Query:
    full query used --> https://shorturl.at/6hpTO
<p align="center">
<img src="https://i.imgur.com/FQn0pYX.jpeg" height="80%" width="80%" alt="Azure Sentinel Tutorial"/>
<br />
<br />

    world map of incoming attacks after 2 hours (built custom logs with geodata included):
<p align="center">
<img src="https://i.imgur.com/HLLVeoj.jpeg" height="80%" width="80%" alt="Azure Sentinel Tutorial"/>
<br />
<br />

