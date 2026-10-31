# Microsoft-Defender

<h2>Description</h2>
Project consists of my Microsoft defender hands-on walkthrough, Onboarding the virtual machine to MDE-Connecting the VM to Microsoft Defender for Endpoint so that it reports telemetry and alerts , VM Isolation- Isolating the compromised Virtual Machine from the network to contain a threat while keeping it reachable for investigation, VM Investigation- Reviewing the alerts, device timeliness and process activity to understand what happened, Log Generation-Production of test activity to detect and analyze and Log Observation- Finding and reading the events in Defender and Sentinel including basic KQL queries
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 
- <b>Diskpart</b>

<h2>Tools and Environments Used </h2>

- <b>Microsoft Defender for Endpoint</b>
- <b>Microsoft Sentinel(SIEM)
- <b>Virtual Machine used as the lab endpoint
- <b>KQL for log queries

<h2>Program walk-through:</h2>

<p align="center">
STEP 1----Onboarding of the VM to MDE(Microsoft Defender for Endpoint) <br/>
<img src="https://i.imgur.com/ngEA1WU.png" height="80%" width="80%">
  
<br />STEP 2--- Isolating the VM

<b> (i) Disabling the Windows Defender Firewall in the VM so that it can reply when the IP address is "pinged"
<img src="https://i.imgur.com/dOPA608.png" height="80%" width="80%"/>

<br /> (ii) Network Security Group(NSG) is enabled to allow all traffic from the internet
<img src="https://i.imgur.com/VfXVOoh.png" height="80%" width="80%"/>

<br /> (iii) Pinging of the VM's public IP address on my personal device
<img src="https://i.imgur.com/VahxxSq.png" height="80%" width="80%"/>

<br /> (iv) Isolating of Personal device through the MDE portal to stop the pings in (iii)  <br/>
<img src="https://i.imgur.com/1wWnGUs.png" height="80%" width="80%"/>
<img src="https://i.imgur.com/mEXk1Jw.png" height="80%" width="80%"/>

<br /> (v) Release of the device from Isolation
<img src="https://i.imgur.com/VxIogeF.png" height="80%"/>

<br />STEP 3--- Log Investigation

<b> (i)Create an Investigation Package
<b> (a) Creation of folder on the VMs desktop with files in it and installation of a browser(Tor Brower)-This enables device network connection table to get logsn device file events table to creating logs(because of the creation of files on the desktop),the process events table is getting logs because edge was opened and installation of the Tor browser- all these are creating logs in defender
<img src="https://i.imgur.com/GNX0am7.png" height="80%" width="80%"/>

<br> (ii) Collection of investigation package for the device- This is done by logging in to the MDE
<img src="https://i.imgur.com/gnqi08T.png" height="80%" width="80%"/>
<img src="https://i.imgur.com/B3U8aK2.png" height="80%" width="80%"/>

<br />STEP 4---Log Generation

<b> (i) DeviceLogEvent

Goal: Generated an authentication event to be able to see the records

Task :Connected to the Virtual Machine via RDP (Remote Desktop Protocol, or Azure Bastion, )
<img src="https://i.imgur.com/hMHBAHS.png" height="80%" width="80%"/>      

<b> (ii) DeviceProcessEvents

Goal: Started a process and captured its command line and parent.

Task : Opened cmd and run a harmless command that creates a clear parent-child chain
<img src="https://i.imgur.com/3FHayNV.png" height="80%" width="80%"/>   

<b> (iii) DeviceNetworkEvents

Goal: Made an outbound connection and see the destination logged.

Task : From PowerShell, a plain HTTPS request was sent to a benign, easily recognisable destination so it stands out in the results:
<img src="https://i.imgur.com/f1A95f1.png" height="80%" width="80%"/>

<b> (iv) DeviceFileEvents

Goal: Create a file in a staging-style location and capture the write.

Task : Write a harmless file into the Temp directory (the same folder the implant used in Module 1):
echo benign-lab-test > C:\Windows\Temp\labtest.txt

To also get a hash recorded, drop a copy of an existing executable instead:
copy C:\Windows\System32\notepad.exe C:\Windows\Temp\labtest.exe
<img src="https://i.imgur.com/OCyr7fq.png" height="80%" width="80%"/>  

<b> (v) DeviceRegistryEvents

Goal: Write an autostart (Run key) value and observe the registry change.

Task : Add a Run key value pointing at a benign program, mirroring the persistence stage without any malware. Then remove it:
<img src="https://i.imgur.com/EcfvlRH.png" height="80%" width="80%"/> 

<b> (vi) DeviceEvents

Goal: Trigger a structured sensor event — a scheduled task creation.
DeviceEvents is the catch-all for typed sensor events that don’t have a dedicated table. Creating a scheduled task raises a clean ScheduledTaskCreated action here (a service install would raise ServiceInstalled the same way).

Task : Create a harmless daily task
<img src="https://i.imgur.com/OksSJmt.png" height="80%" width="80%"/> 


<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
