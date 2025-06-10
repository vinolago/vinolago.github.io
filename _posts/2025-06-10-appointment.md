---
title: "Appointment - HTB Catch the Flag"
layout: single
date: 2025-06-10
categories: [blog]
teaser: /assets/images/appoint-pawned.png
tags: [hack the box, Cap]
excerpt: ""
---
### Overview

![Appointment](/assets/images/appoint-pawned.png)

Appointment is a (very easy) target machine containing a back-end database that is vulnerable. My goal is to attack it with SQL Injection. 

### Skills Learned
- Web enumeration
- SQL Injection

### Ports enumeration

First we start with an nmap scan to find open ports. We see that port 80 is open and it’s running Apache 2.4.38. 

<img src="/assets/images/appoint-nmap.png" alt="Nmap Scan" style="max-width:100%;">

Let’s see the web server on a browser. And it’s a login page. Now the next goal is to find the login credentials.

<img src="/assets/images/appoint-login.png" alt="Login form" style="max-width:100%;">

I tried a brute-force attack using gobuster to find hidden web directories but nothing interesting came up. 

<img src="/assets/images/appoint-gobuster.png" alt="Gobuster" style="max-width:100%;">

Next I tried to login by manipulating input credentials through SQL Injection. 
If the SQL database is misconfigured (i.e no input validation), we can comment out (#) the password of the admin and see if it bypasses the login. And it does!

_(The admin’# will search for the admin username but comment out the rest of the query, i.e password)_.

Now we see the flag

<img src="/assets/images/appoint-flag.png" alt="Flag" style="max-width:100%;">
