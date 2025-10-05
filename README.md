🔐 Brute Force Detection Using Splunk

📘 Project Overview

This project demonstrates how to use Splunk Enterprise to detect and visualize brute-force login attempts by analyzing Windows Security Event Logs. The objective was to simulate multiple failed login attempts and build automated detection and alerting mechanisms within Splunk.


---

⚙️ Setup and Configuration

1. Environment

Host: Windows 10 Virtual Machine

SIEM: Splunk Enterprise

Forwarder: Splunk Universal Forwarder

Log Sources: Security, System, Application


2. Configuration Steps

1. Installed Splunk Enterprise (Indexer/Search Head).


2. Installed Splunk Universal Forwarder on Windows 10 VM.


3. Configured inputs.conf to forward Windows Event Logs:

[WinEventLog://Security]
disabled = 0
[WinEventLog://System]
disabled = 0
[WinEventLog://Application]
disabled = 0


4. Verified data ingestion with:

index=main | stats count by sourcetype




---

🔍 SPL Query for Detection

index=main sourcetype="WinEventLog:Security" EventCode=4625
| stats count by Account_Name, Workstation_Name, IpAddress
| where count > 5
| sort - count

Explanation:
This SPL query identifies accounts or IP addresses with more than 5 failed login attempts — a strong indicator of brute-force activity.


---

📊 Dashboard and Visualization

Dashboard Panels:

Failed Logins Over Time

Top Targeted Accounts

Top Source IPs

Attack Trend Chart


You can create this in Dashboard Studio for a clean, modern visualization.

Example Dashboard Query:

index=main sourcetype="WinEventLog:Security" EventCode=4625
| timechart span=5m count by Account_Name


---

⚠️ Alert Configuration

Alert Name: Brute Force Attack Detected
Trigger Condition: >5 failed logins within 5 minutes
Action: Send email or Slack notification to security admin


---

🧾 Incident Report Summary

Incident: Multiple failed login attempts detected on Win10-VM
Detection Source: Splunk Enterprise Dashboard
Response: Investigated logs, identified attack pattern, and validated alert
Outcome: Detection successful; alert configuration validated


---

💡 Key Skills Demonstrated

SIEM configuration and log forwarding

SPL query design for attack detection

Dashboard creation and data visualization

Security alerting and incident response workflow

Documentation and reporting

---

🧰 Tools Used

Tool	Purpose

Splunk Enterprise	SIEM platform for data analysis
Universal Forwarder	Log collection agent
Windows Event Viewer	Source of Security logs
PowerShell	Simulation of failed logins
Dashboard Studio	Visualization interface

---

🧠 Learning Outcome

Through this project, I gained hands-on experience in:

Threat detection using SIEM tools

SPL-based log correlation

Building a security monitoring dashboard

Real-world alert creation and validation
