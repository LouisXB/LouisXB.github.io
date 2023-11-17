## Cloud Security Analyst Project Blog

In this blog I'll be detailing a recent project I completed in Microsoft Azure.

### Tools Used: 
Azure Sentinel (SIEM), Log Analystics wWrkspace, Azure Virtual Machine, Powershell

In the ever-evolving landscape of cybersecurity, understanding the tactics of threat actors is crucial. One innovative approach is the use of honeypots - decoy systems 
designed to lure and analyze unauthorized access attempts. In this blog, I'll share my journey of creating a honeypot VM (Virtual Machine) in Microsoft Azure to capture 
real-time attack data, offering a fascinating glimpse into the world of digital intruders.

### Project Overview:
The project's heartbeat was a honeypot VM in Azure, exposed to the internet to attract threat actors. This setup allowed me to record failed Remote Desktop Protocol (RDP) 
login attempts, offering real insights into attack patterns. Key tools from the Microsoft Azure suite played a pivotal role, including Azure VM, Azure Sentinel, and Log 
Analytics Workspace, along with a custom PowerShell script.

### Step-by-Step Guide:

Setting Up the Honeypot VM:
I initiated the project by deploying a Windows VM inside the Azure Portal. I created a username and password which I used to connect to my VM via Remote Desktop Connection. 
Given the VMs role as a honeypot, once logged in to it, I intentionally disabled the firewall, ensuring it was completely exposed yet monitored. Having a VM that is completely 
exposed draws in attackers from all across the globe.

### Capturing Attack Data:
Inside the VM, I employed a PowerShell script tailored to log failed RDP login attempts, storing this data in a file named failed_rdp.log. The Powershell script created a set of 
sample data, and appended all new failed logins below. Additionally, the Powershell script integrated with an IP Geolocation API to take the attackers IP addres and 
provide the geolocations (city, longitude, latitude, etc.), adding it to the log data. This file became the cornerstone of my data collection.

###Integration with Azure Analytics Workspace:
The VM was then integrated with Azure Log Analytics Workspace. Here, I created a custom MMA-based log, fed with the failed_rdp.log data, and provided a source path back to the failed_rdp.log 
on the VM located at C:\ProgramData\Failed_rdp.log

### Leveraging Azure Sentinel:
The next phase involved connecting the Log Analytics Workspace to Azure Sentinel. This connection was crucial for retrieving the log data from the honeypot VM, providing 
a streamlined data flow.

### Alert Rule Configuration:
In Azure Sentinel, I configured a custom incident alert rule. This rule was designed to trigger notifications upon detecting issues related to failed credential access, 
a common sign of intrusion attempts.

### Results and Analysis:
The data harvested was eye-opening, seeing attacks from across the world in Singapore. The failed_rdp.log revealed varied attack patterns and techniques, highlighting the persistence 
and sophistication of some threat actors. This exercise underscored the importance of robust security measures in the face of persistent cyber threats.

### Conclusion:
This project was not just about building an Azure honeypot but about understanding the nature and frequency of cyberattacks in a real-world scenario. It highlighted the effectiveness 
of Azure tools in creating virtual enviornments, capturing/logging data, and alerting on events.

### Additional Resources:
For those interested in delving deeper or replicating this project, I've included the YouTube link below. The orginal creator of this project is Josh Madakor, an instructor 
and Cybersecurity professional

Link: https://youtu.be/RoZeVbbZ0o0?si=l2gU3S7cq-zfCFql

Powershell Script: https://github.com/joshmadakor1/Sentinel-Lab/blob/main/Custom_Security_Log_Exporter.ps1

