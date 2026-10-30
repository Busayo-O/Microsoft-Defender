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

<br />STEP 3--- Create an Investigation Package

<b> (i) Creation of folder on the VMs desktop with files in it and installation of a browser(Tor Brower)-This enables device network connection table to get logsn device file events table to creating logs(because of the creation of files on the desktop),the process events table is getting logs because edge was opened and installation of the Tor browser- all these are creating logs in defender
<b> (ii) Collection of investigation package for the device- This is done by logging in to the MDE
<img src="https://i.imgur.com/GNX0am7.png" height="80%" width="80%"/>
<br />
<br />
Sanitization complete:  <br/>
<img src="https://i.imgur.com/K71yaM2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://i.imgur.com/AeZkvFQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
Wait for process to complete (may take some time):  <br/>
<img src="https://i.imgur.com/JL945Ga.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Sanitization complete:  <br/>
<img src="https://i.imgur.com/K71yaM2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://i.imgur.com/AeZkvFQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>




<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
