---
title: "Cap - HTB Catch the Flaf"
layout: single
permalink: /projects/cap/
---

### 🧠 Overview

So, in this lab, I attempt to hack the **HTB Cap Machine**. It's a retired machine and marked as easy. 

### 🔧 Skills learned
- Web enumeration
- Packet capture analysis
- IDOR
- Exploiting Linux capabilities

### Enumerating the application

I started my enumeration by conducting nmap scap. We see 3 ports open:

<img src="/assets/images/nmap-scan-1.png" alt="Nmap Scan Screenshot" style="max-width:100%;">

The HTTP nmap scan reveals port 80 is running Gunicorn server. Let’s browse to that page. We see a dashboard.

<img src="/assets/images/dashboard-2.png" alt="Dashboard" style="max-width:100%;">

Browsing to page, we see output of ipconfig while network status shows the output of netstat command. I navigated to _Security Snapshot menu_, then changed data ID from 2 to 0 to see any data by another user. This is called Insecure Direct Object Reference (DOR) exploitation.

<img src="/assets/images/pcap-download.png" alt="pcap" style="max-width:100%;">

Then I downloaded the pcap file and analysed it on Wireshark.
And there in plain text we see the credentials for user Nathan being transmitted via ftp.

<img src="/assets/images/wireshark-analysis.png" alt="Wireshark" style="max-width:100%;">

I then tried to authenticate the credentials with an ssh login into the system. The login is successful!

<img src="/assets/images/ssh-nathan.png" alt="SSH Successful" style="max-width:100%;">

### Privilege escalation

First, I started an Apache2 service (./lineapeas.sh python -m http-server 80) then tried to escalate privilege using curl.

<img src="/assets/images/linpeas-results.png" alt="linpeas.sh" style="max-width:100%;">

Then exploited the python3.8 capabilities directory (usr/bin/python3.8). Since python3.8 has setuid capability, it means the root user has allowed python3 to be run by all users. This is very dangerous. 

We exploit by switching to UID 0, which effectively is the root. The Python command is as follows:

_import os 
os.setuid(0) 
os.system("/bin/bash")_

<img src="/assets/images/privilege-escalated.png" alt="Root" style="max-width:100%;">

Basically what we’ve done is used Python3’s os module to change our UID to 0, or root, and then spawn a shell.
Then we grab the flags.

<img src="/assets/images/flags.png" alt="Flags" style="max-width:100%;">


