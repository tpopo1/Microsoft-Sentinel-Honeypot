# Description
The purpose of this lab was to see how quickly malicious actors swarm to a vulnerable machine on the internet. I provisioned a Windows 10 VM, and opened up the firewall to make it vulnerable to attacks. I also provisioned a Log Analytics Workspace group in Azure and associated it with the VM to ingest logs from event viewer into it. With the assistance of my PowerShell script I was able to parse the failed RDP attempts, and pinpoint the origin country by using a third party API that collects geographic location of the threat actor.

I provisioned an instance of Azure Sentinel (SIEM) to visualize the RDP failures on a world map. The visualization is retrieving data from the log analytics workspace that was setup, while the workspace is being fed data by the PowerShell script. It's akin to a symbiotic relationship, all these parts need the help of the others to function properly.

# Event Viewer/IP Geolcation API
<p align="center">
  <img src="https://i.imgur.com/fmmSN5L.png" />
</p>

The image above is that of a security log detailing a failed login event, and the third party API geolocation tool that was used for this project. As you can see the geolocation tool highlights the location based on the IP address of the device that initiated the RDP session. It starts at a very high level, then it quickly gets granular, even detailing the longitude and latitude of the IP.

# Languages Utilized
- <b>PowerShell:</b> A PowerShell script was used to extract failed rdp attempt logs from event viewer to ingest into Log Analytics Workspace in Microsoft Azure.

# Tools Utilized
- <b>ipgeolocation.io:</b> This tool translates IP addresses to an orignating geographic location with API calls.

# Attacks flooding in from the Netherlands; Logs with geodata being output in Powershell
<p align="center">
  <img src="https://i.imgur.com/vZYiXCp.png" />
</p>

In the graphic above you can see that once I opened the firewall requests started to flood in. Most notably, the Netherlands was the first country to make a persistent effort in trying to get into the VM. This person in particular tried to RDP into the device as the admin. Their spelling of administrator should be noted " administrateur". Although this is a tiny detail, the nuance matters when trying to brute force a device.

# World map of failed rdp attempts after 3-4 hours
<p align="center">
  <img src="https://i.imgur.com/Vga5dvA.png" />
</p>

Depicted in the graphic above is a world map highlighting the areas where the failed rdp attempts originated from. The Key players include Panama, Hong Kong, and Russia. Roughly 3400 failed rdp attempts were captured by Log Analytics Workspace and Azure Sentinnel, but there were MANY more attempts before I was able to get everything working correctly. The real number of failed attempts would be in the ballpark of 6000-7000.


credit goes to joshmadakor1 as the original creator of this lab.
