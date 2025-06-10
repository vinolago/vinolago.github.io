---
layout: single
title: "Projects"
permalink: /projects/
author_profile: true
---
## Projects
Here are some of the projects I've worked on:

### [Cap](/projects/cap/)

### 🔐 Project Title: Build a Home SOC Lab & Detect a Simulated Attack

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



{% include feature_row id="project_cards" %}

