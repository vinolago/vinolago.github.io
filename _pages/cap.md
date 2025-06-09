---
title: "Cap - HTB Catcg the Flaf"
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
I started my enumeration by conducting nmap scap. We see 3 ports open,
nmap img

The HTTP nmap scan reveals port 80 is running Gunicorn server. Let’s browse to that page. We see a dashboard.
Dashboard img

Browsing to ipconfig, we see output of ipconfig while network status shows the output of netstat command, which we can download.
pcap-download

Then I downloaded the pcap file and analysed it on Wireshark.

And there in plain text we see the credentials for user Nathan being transmitted via ftp.
Wireshark img

I then tried to authenticate the credentials with an ssh login into the system. The login is successful!
Ssh-img

### Privilege escalation
First, I started an Apache2 service (./lineapeas.sh python -m http-server 80) then tried to escalate privilege using curl.
Lineas img

Then exploited the python3.8 capabilities directory (usr/bin/python3.8). Since python3.8 has setuid capability, it means the root user has allowed python3 to be run by all users. This is very dangerous. 

We exploit by switching to UID 0, which effectively is the root. The Python command is as follows:

import os 
os.setuid(0) 
os.system("/bin/bash")

Privilege img

Basically what we’ve done is used Python3’s os module to change our UID to 0, or root, and then spawn a shell.
Then we grab the flags.
Flags img


### 📸 Screenshot

![scanner output](/assets/images/nmap.png)
