---
title: "Crocodile Writeup"
layout: single
date: 2025-06-13
categories: [blog]
teaser: /assets/images/croc-pawned.png
tags: [hack the box, Cap]
excerpt: ""
---

![Crocodile](/assets/images/croc-pawned.png)

### Overview

For this machine, I started with an nmap scan. Port 21 and Port 80 are open and we can also see the services (and version) each port runs.

<img src="/assets/images/croc-nmap.png" alt="Nmap Scan" style="max-width:100%;">

Crucially, this server allows ftp anonymous login, which is fantastic!

<img src="/assets/images/croc-anon.png" alt="Anonymous login" style="max-width:100%;">

Now that we’ve logged in, let’s explore the system and retrieve the flag. We see two interesting files in our currency directory, which we can download into our machine and view.

The above users and passwords could help us escalate privileges or even log into the HTTP server that we saw open at port 80 (Apache httpd 2.4.41). The web page displayed at port 80 is as shown:

I tried navigating the pages to find any direct path to attacking the server, but it led to nowhere. Even Wappalyzer didn’t help.

Next I attempted to enumerate hidden directories using gobuster (-x filters out unnecessary files). What we’re looking for is an admin panel that can give us a foothold (using the credentials we obtained from ftp).

<img src="/assets/images/croc-gobuster.png" alt="Gobuster" style="max-width:100%;">

At last, we found a /login.php page. Let’s try to login (luckily only 4 credentials to attempt!)

<img src="/assets/images/croc-login.png" alt="Login" style="max-width:100%;">

We’ve managed to login with admin credentials since we can now see a Server Manager admin panel.

<img src="/assets/images/crco-dir.png" alt="Directories" style="max-width:100%;">

Let’s retrieve the flag

<img src="/assets/images/croc-cat.png" alt="Flags" style="max-width:100%;">
