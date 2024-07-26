<h1>Windoes Event Log Analysis in Splunk (In Progress)</h1>



<h2>Description</h2>In this hybrid walkthrough lab, I was tasked with investigating a user suspected of taking malicious actions on the machine. I was given several Windows Event Log files and decided to upload the data into Splunk for a more efficient searching experience. Once the Event Logs were properly displayed in Splunk, the first part of my investigation was to determine when the user first logged in. Using Search Processing Language (SPL), I changed the source to Windows Security Logs with Event ID 4624, which logs successful logins. Once the exact time the user logged in was determined, it was hinted that the user had changed the native firewall rules. I then switched the source logs to Windows Firewall and immediately discovered a suspicious, likely malicious log where the added firewall rule read "Metasploit C2 Bypass." However, the user was listed as "NOT_TRANSLATED." To determine if the malicious user added the rule, I went back to the original login log and found their Security Identifier (SID), a unique identifier assigned to users when logged in. The SID matched the Modifying User's SID in the Firewall log, confirming it was the same user. Furthermore, it was stated that the native antivirus detected a threat, which I was to investigate further. Changing the source logs to Windows Defender and researching the Event IDs related to Windows Defender, Event IDs 1116 and 1117, revealed that the antivirus detected and quarantined the hacktool SharpHound, which is used in Active Directory enumeration. 
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
Next, it was revealed the native anti-virus idnetified a threat and performed actions what it found. With that knowledge, I again researched for Event IDs relted to Windows Defender, and came accross two 1116 and 1117. Within Splunk changing the source of logs to Windows Defender Operational with the Event ID 1116, I discovered Windows Defender detected the hack tool called SharpHound. With Evend ID 1117, it showed that 100% of actions performed by Windows Defenders were quartining files adn programs meaning that SharpHound was quarintined. <br/>
<img src="https://github.com/user-attachments/assets/a7f0e0e0-01e2-4a5d-a103-b606aef328f0" height="100%" width="100%" alt="Windows Event Logs in Splunk"/>
<img src="https://github.com/user-attachments/assets/ae3f003b-653b-468a-95f6-61416696c550" height="100%" width="100%" alt="Windows Event Logs in Splunk"/>
<img src="https://github.com/user-attachments/assets/022465bf-2eab-4b86-a8c7-3bc00dc687ee" height="100%" width="100%" alt="Windows Event Logs in Splunk"/>
<br />
<br />
The last question mentioned that it is suspected that the malicious user had deleted some logs and I was to find out which ones. I again researched teh Event ID for Event Logs being delted and found it to be Event ID 104, and querying for that in Splunk showed that in within the time of cyberjunkie being logged in, the Microsoft-Windows-Windows Firewall With Advanced Security/Firewall Logs were cleared.<br/>
<img src="https://github.com/user-attachments/assets/0379cab3-c947-41f3-bafb-9961c628bc2f" height="100%" width="100%" alt="Windows Event Logs in Splunk"/>
<br />
<br />

<h2>Thoughts</h2>
This lab was a great refresher and practice in Windows Event Log investigations. Considering that most end users utilize Windows endpoints, being able to use the Event Logs is a valuable skill, especially if Sysmon or any other non-native logging agent is not present on the machine. While I chose to upload the Event Logs into Splunk and query them with SPL, I believe this approach is reasonable. It was simple and aligns with the role of a SOC Analyst, which involves using tools to assist in investigations. The questions in the lab were easy to follow, and I did not encounter any significant issues. If there was an Event ID I did not recognize, I could easily search for it online, where there are ample resources to find the necessary information. Overall, this was an easy yet beneficial lab to complete.
<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
