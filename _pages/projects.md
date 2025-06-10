---
layout: single
title: "Projects"
permalink: /projects/
author_profile: true
---
## Projects
Here are some of the projects I've worked on:

### 🔐 Project 1: Build a Home SOC Lab & Detect a Simulated Attack

Summary:
Set up a lightweight SOC lab to monitor Windows logs using Sysmon and detect simulated attacks with Atomic Red Team. Demonstrates skills in log collection, attack simulation, detection, and reporting.

🧰 Tools & Technologies
Windows 10 VM

Sysmon

Wazuh (or ELK Stack)

Atomic Red Team

MITRE ATT&CK

🗺️ Lab Architecture

One Windows VM sends logs to Wazuh. Simulated attack executed on host to trigger detection.

⚔️ Attack Simulated
Technique: T1059 - Command and Scripting Interpreter
Command Used:

powershell
Copy
Edit
powershell -enc <base64 encoded malicious script>
🔍 Detection Evidence

Alert raised in Wazuh for suspicious PowerShell execution

Sysmon Event ID 4104 captured decoded command

✅ Findings & Response
IOC: Suspicious base64-encoded PowerShell

Detected by: Sysmon + Wazuh rules

Response: Logged, investigated, and verified with MITRE mapping

Lessons Learned: Validated EDR detection capability with low-resource tooling

📚 MITRE Mapping
Tactic	Technique	ID
Execution	PowerShell	T1059.001
Defense Evasion	Obfuscated Files or Info	T1027

### 📨 Project 2: Phishing Email Investigation & IOC Analysis

### Summary:
Analyzed a real-world phishing email sample to extract indicators of compromise (IOCs), investigate malicious URLs and attachments, and write a concise report for triage and escalation purposes.

### 🧰 Tools & Platforms
VirusTotal

URLScan.io

MXToolbox (for email header analysis)

PhishTool (email analyzer)

AbuseIPDB

Markdown & Google Docs for report

📩 Phishing Sample Overview
Field	Value
Sender Email	no-reply@fakebankingalert.com
Subject	"Action Required: Verify Your Account Now"
Attachment	invoice.html
Received Date	June 2025

🔍 Investigation Steps
Extracted email headers using PhishTool

Parsed links and attachments from the HTML file

Queried URLs and file hashes via VirusTotal

Identified indicators matching known phishing kits

Documented MITRE mapping and recommended next steps

🧪 Sample IOCs Identified
Type	Value	Source
URL	hxxp://secure-alert[.]co/login	URLScan.io
SHA256	a9c3f2e4f87...	VirusTotal
IP	185.203.119.22	AbuseIPDB

🧭 MITRE ATT&CK Mapping
Tactic	Technique	ID
Initial Access	Phishing: Spearphishing Link	T1566.002

🧾 Findings
The email spoofed a financial institution and linked to a fake login portal.

The attachment included JavaScript that redirected to a credential-harvesting site.

The server hosting the site had been flagged for malware by multiple vendors.

{% include feature_row id="project_cards" %}

