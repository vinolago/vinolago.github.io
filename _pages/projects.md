---
layout: single
title: "Projects"
permalink: /projects/
author_profile: true
---
## Projects
Here are some of the projects I've worked on:

### 🔐 Project 1: SOC Lab for Detecting a Simulated Attack

Summary:

- Set up a lightweight SOC lab to monitor Windows logs using Sysmon and detect simulated attacks with Atomic Red Team. Practiced skills in log collection, attack simulation, detection, and reporting.

### 🧰 Tools & Technologies
 - Windows 10 VM
 - Sysmon
 - Wazuh
 - Atomic Red Team
 - MITRE ATT&CK

🗺️ Lab Architecture

One Windows VM sends logs to Wazuh. I executed simulated attack on host PC to trigger detection.

⚔️ Attack Simulated
Technique: T1059 - Command and Scripting Interpreter
Command Used:

powershell -enc <base64 encoded malicious script>

### 🔍 Detection Evidence

 - Alert raised in Wazuh for suspicious PowerShell execution
 - Sysmon Event ID 4104 captured decoded command

### ✅ Findings & Response
 - IOC: Suspicious base64-encoded PowerShell
 - Detected by: Sysmon + Wazuh rules
 - Response: Logged, investigated, and verified with MITRE mapping
 - Lessons Learned: Validated EDR detection capability with low-resource tooling

### 📚 MITRE Mapping

| Tactic             | Technique                    | ID     |
|--------------------|------------------------------|--------|
| Privilege Escalation | Exploitation for Priv Esc   | T1068  |
| Initial Access     | Exploit Public-Facing App    | T1190  |


-------------------------------------------------------------------------------------------------------

### 📨 Project 2: Phishing Email Investigation & IOC Analysis

### Summary:

Analyzed a real-world phishing email sample to extract indicators of compromise (IOCs), investigate malicious URLs and attachments, and write a concise report for triage and escalation purposes.

### 🧰 Tools & Platforms
 - VirusTotal
 - URLScan.io
 - MXToolbox (for email header analysis)
 - PhishTool (email analyzer)
 - AbuseIPDB

### 📩 Phishing Sample Overview

| Field           | Value                                         |
|------------------|-----------------------------------------------|
| Sender Email     | no-reply@fakedbankingalert.com                |
| Subject          | Action Required: Verify Your Account Now     |
| Date Received    | June 7, 2025                                  |
| Attachment       | invoice.html                                  |
| Embedded Link    | hxxps://secure-alert[.]co/login               |


### 🔍 Investigation Steps
 - Extracted email headers using PhishTool
 - Parsed links and attachments from the HTML file
 - Queried URLs and file hashes via VirusTotal
 - Identified indicators matching known phishing kits
 - Documented MITRE mapping and recommended next steps

### 🧪 Sample IOCs Identified

| Type     | Value                               | Source         |
|----------|-------------------------------------|----------------|
| URL      | hxxps://secure-alert[.]co/login     | URLScan.io     |
| SHA256   | a9c3f2e4f87abc767rty09afcde         | VirusTotal     |
| IP       | 185.203.119.22                      | AbuseIPDB      |
| Filename | invoice.html                        | Email attachment |


### 🧭 MITRE ATT&CK Mapping

| Tactic         | Technique                   | ID         |
|----------------|------------------------------|------------|
| Initial Access | Phishing: Spearphishing Link | T1566.002  |
| Command & Control | Obfuscated Files/Information | T1027    |


### 🧾 Findings
 - The email spoofed a financial institution and linked to a fake login portal
 - The attachment included JavaScript that redirected to a credential-harvesting site
 - The server hosting the site had been flagged for malware by multiple vendors

-------------------------------------------------------------------------------------------------------

### 🛡️ Project 3: Vulnerability Assessment with Nessus Essentials

### Summary:
 - Conducted a full vulnerability scan of a Metasploitable2 virtual machine using Nessus Essentials
 - Identified vulnerabilities by severity and created a risk-based remediation report

### 🧰 Tools Used
 - Nessus Essentials
 - Metasploitable2 (Linux)
 - CVSS Calculator
 - Kali Linux (for scanning)

### 🧪 Scan Details

| Target | 192.168.56.101 (Metasploitable2) |
| Scanner | Kali Linux (Nessus Essentials) |
| Scan Profile | Basic Network Scan |
| Duration | ~10 minutes |

### 📉 Top Vulnerabilities Found

| Vulnerability           | CVE ID        | CVSS Score | Affected Service | Recommendation                              |
|--------------------------|---------------|------------|------------------|----------------------------------------------|
| Apache Struts RCE        | CVE-2017-5638 | 9.8        | Web Server       | Update Apache or remove vulnerable plugin    |
| Linux Kernel Priv Esc    | CVE-2009-2692 | 10.0       | Kernel           | Upgrade kernel to patched version            |
| Tomcat Auth Bypass       | CVE-2010-0738 | 8.6        | App Server       | Restrict access, upgrade Tomcat              |


### 🧭 Risk Prioritization
 - Critical vulnerabilities allow local or remote code execution
 - The system lacks segmentation, increasing attack surface
 - Immediate patching or isolation of this host is recommended.

### 🧾 Deliverables
 - Executive summary of vulnerabilities
 - Risk matrix (CVSS score vs. asset criticality)
 - Remediation plan for each major finding

{% include feature_row id="project_cards" %}

