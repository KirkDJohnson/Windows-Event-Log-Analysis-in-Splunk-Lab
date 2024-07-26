<h1>Windoes Event Log Analysis in Splunk (In Progress)</h1>



<h2>Description</h2> Text
<br />


<h2>Languages and Utilities Used</h2>

- <b>Splunk Search Processing Language</b> 
- <b>Windows Event Logs</b>
- <b></b>

<h2>Environments Used </h2>

- <b>Oracle Virtual Box for Virtual Machine</b>
- <b>Windows 10 </b>

<h2>Lab Overview</h2>

<p align="center">
The scenario layed out for the lab/investigation.<br/>
<img src="https://github.com/user-attachments/assets/41affe2e-15e8-4da8-b57e-b80aa706ff97" height="100%" width="100%" alt="Windows Event Logs in Splunk"/>
<br />
<br />
Once I downloaded the lab files and found out they were multiple Windows Event Log files, I decided it would to upload them to SPlunk because it would be easier to seraching and parsing the logs than through the native Windows Event Viewer. to upload into Splunk for an <br/>
<img src="https://github.com/user-attachments/assets/f0ae72d8-2398-42fb-9e38-4ccdb4886f52" height="100%" width="100%" alt="Windows Event Logs in Splunk"/>
 <img src="https://github.com/user-attachments/assets/44f14287-109e-46ed-956e-67c80fd80614" height="100%" width="100%" alt="Windows Event Logs in Splunk"/>
<br />
<br />

Within the questions to answer in the investigation, the first was to discoverd when the user cyberjunkie first logged to begin piecing together the time line. Within Splunk I used the source type Security Logs and filtered fro Event ID/Code 4626 which logs user successfully logging in. The user cyberjunkie was found to first log in at 27/03/2023 14:37:09 UTC time.<br/>
<img src="https://github.com/user-attachments/assets/589241f7-a49f-4a76-a8fe-01cd39d78e7c" height="100%" width="100%" alt="Windows Event Logs in Splunk"/>
<img src="https://github.com/user-attachments/assets/9a61f5f0-709c-4910-b43c-12af82c3cf90" height="100%" width="100%" alt="Windows Event Logs in Splunk"/>
<br />
<br />
The second question hinted that the user has manipulated the firewall, so I changed the source in Splunk to the Firewall Event Logs. The first log was suspicious if not malicious as a rule was added called 'Metasploit C2 Bypass, a popular pentesting tool. However, the user field in the logs displayed "User=NOT_TRANSLATED", so I decided to find the user cyberjunkie's Security Identifier (SID), that is unqiue to users. Once I discovered the SID, I compared it to the Modifying User in the firewall log and proves that the the user cyberjunkie made updated the firewall rule.  <br/>
<img src="https://github.com/user-attachments/assets/40c73209-700e-45f8-aca5-6a6909eb6aa1" height="100%" width="100%" alt="Windows Event Logs in Splunk"/>
<img src="https://github.com/user-attachments/assets/350c66c8-9319-4c25-83f0-fc2432370192" height="100%" width="100%" alt="Windows Event Logs in Splunk"/>
<img src="https://github.com/user-attachments/assets/c2caa0ac-b16d-405e-9fa7-3cf7600d9375" height="100%" width="100%" alt="Windows Event Logs in Splunk"/>
<br />
<br />
The next question metnioned that the user had changed audit policy on the machine and was to discover what was changed. I researched what Event ID would log audit policy changes and found it to be Event ID 4719, and using SPL with that Event ID returned one log that revealed Other Object Access Events was changed by the user.<br/>
<img src="https://github.com/user-attachments/assets/7d283d5c-8499-4abf-b2d9-3892fdd43fd4" height="100%" width="100%" alt="Windows Event Logs in Splunk"/>
<img src="https://github.com/user-attachments/assets/cf5457e5-419d-44b7-9829-fc778ee5add2" height="100%" width="100%" alt="Windows Event Logs in Splunk"/>
<br />
<br />
Text<br/>
<img src="" height="100%" width="100%" alt="Windows Event Logs in Splunk"/>
<br />
<br />
Text<br/>
<img src="" height="100%" width="100%" alt="Windows Event Logs in Splunk"/>
<br />
<br />
Text<br/>
<img src="" height="100%" width="100%" alt="Windows Event Logs in Splunk"/>
<br />
<br />
Text<br/>
<img src="" height="100%" width="100%" alt="Windows Event Logs in Splunk"/>
<br />
<br />
Text<br/>
<img src="" height="100%" width="100%" alt="Windows Event Logs in Splunk"/>
<br />
<br />
Text<br/>
<img src="" height="100%" width="100%" alt="Windows Event Logs in Splunk"/>
<br />
<br />
Text<br/>
<img src="" height="100%" width="100%" alt="Windows Event Logs in Splunk"/>
<br />
<br />
Text<br/>
<img src="" height="100%" width="100%" alt="Windows Event Logs in Splunk"/>
<br />
<br />
Text<br/>
<img src="" height="100%" width="100%" alt="Windows Event Logs in Splunk"/>
<br />
<br />



<h2>Thoughts</h2>
Text
<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
