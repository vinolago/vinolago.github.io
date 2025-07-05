---
title: "DNS Exfiltration Writeup"
layout: single
date: 2025-06-23
categories: [blog]
header:
 teaser: /assets/images/dns-tun.jpg
tags: [Hackathon, DNS, event logs]
excerpt: "DNS exfiltration challenge"
read_time: true
---

### 🧠 Overview

![DNS](/assets/images/dns-tun.jpg)

This is one of the CTF challenges I tackled as part of the 2025 Dewald Roode Cybersecurity Hackathon. 

### Problem:

A compromised host on the network is exfiltrating sensitive data by tunneling it over DNS queries to an external, attacker-controlled domain. Your task is to identify the compromised host, reconstruct the exfiltrated data, and ultimately find the flag.

### Enumeration

What we need to look for is: 1) a host that is making a high number of DNS requests in a short time or 2) domains with long, random-looking subdomains. 

Let’s do just that by analysing the PCAP file on Wireshark. There’s only one IP (192.168.1.74) that has issued  DNS requests as shown below. 

<img src="/assets/images/wshark1.png" alt="Wireshark" style="max-width:100%;">

Now let’s extract DNS queries from this IP and save in a file named queries.txt. Then we clean the data so that we have only Base64 (remove any domains present). The next script command joins the base64 parts into one line.

<img src="/assets/images/base64d2.png" alt="Base64" style="max-width:100%;">

Next, we inspect the base64 string above to decode it. After the 0-, the rest of the code is clearly Base64. 

Q1RGe1RVTk4zTEwxTkdfRE5TX0wxSzNfNF9QUjB9

### Decode Base64

To decode the base64 we use: 

<img src="/assets/images/flag3.png" alt="DNS Traffic" style="max-width:100%;">

### 🎉 That's our flag!

Now we can answer the following questions:

### What is the full domain name used by the attacker for data exfiltration?
Crazzyc4t[.]com

So the attacker likely registered crazzyc4t[.]com and configured it to receive and log DNS queries for exfiltration. 

### What encoding method was used for the exfiltrated data within the DNS queries?
Base64

### What type of DNS record did the attacker use for data exfiltration
The query type is A

### Key Lessons We Learned
 - This attack incident was an exfiltration over DNS.
 - Attackers encoded data into the subdomain of a DNS query and sent it to a domain they control (crazzyc4t[.]com). The attacker’s server logs this query and decodes the base64 chunk.
 - This query typically asks for an A record, which resolves a domain to an IP address (attackers can also use TXT or MX records).
