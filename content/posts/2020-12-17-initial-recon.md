+++
title = "Initial Reconnaissance with nmap, nikto and gobuster"
date = "2020-12-17"
description = "How to do initial reconnaissance on a webserver with nikto, nmap and gobuster"
tags = ["Cybersecurity"]
+++

# Introduction
Greetings peeps. Today I want to talk about something mundane. The scenario is, you have the permission to scan a friend's/client's web app, you are running Kali and want to do some essential tests before going full akimbo.

I can't stress enough the part where you got your permission. Remember kids, applying cybsec tools on a machine you don't have permission to is icky, bad and totally not recommended. And what I am going to discuss here - however harmless they are - should be taken in this context. 

With that out of the way let's begin

# Nmap
I love nmap, network mapper if we want to be verbose. It is really the swiss army of the cybersecurity field. We often use it for port scanning and enumeration but with its scripting capability it also can do some proper penetration testing. But today we are going to apply its scanning and enumeration features. 

I often do a staged testing. I learned about it from Heath "Cybermentor" Adams' course - which is something I definitely recommend - and it goes like this. 

First, we do a run of the mill port scan:

	sudo nmap -sS -vvvv -T4 <ip_address>

This finishes veery quickly, we can also add a `-p-` to do a full port scan but for our purposes the default application is okay. This will give us some open ports, hopefully. We note down these ports and use them in the enumeration scan:

	sudo nmap -sV -p<found,ports,by,comma> -vvvv -T4 <ip_address>

With this, we don't spend time on the ports we know that are already closed and focus on the open ports. Of course we can also use, and this may be the third stage, the `-A` switch instead of `-sV`:

	sudo nmap -A -p<again, them, ports> -vvvv -T4 <ip_address>

As you already know, this usage is very noisy - which is something we want as a pentester. Blue team - the client's network security team - should detect and catch us if they can, if not this goes in the findings pile. `-A` does all the enumeration tricks nmap has, including OS fingerprinting. But bear in mind that it can be misled. Needless to say, to double check it we can use other tools. But the scope of this writing is web servers. We assume that we found an up and running webserver on port 80, 443 or 8080 and when we move to that address with our browser we see a webpage of sorts. 

Now comes the fun part, nikto and gobuster.

# Nikto
Nikto is a funny tool to me, because it means "nobody" in Russian and that amuses me for some reason. Anyway, nikto is very easy to use. We only point the thing and fire away:

	nikto -host <ip_address> -o <output_file> -Format htm

This will create a html file in the desired filename. We can also add scan tuning options:


	1     Interesting File / Seen in logs
        2     Misconfiguration / Default File
        3     Information Disclosure
        4     Injection (XSS/Script/HTML)
        5     Remote File Retrieval - Inside Web Root
        6     Denial of Service
        7     Remote File Retrieval - Server Wide
        8     Command Execution / Remote Shell
        9     SQL Injection
        0     File Upload
        a     Authentication Bypass
        b     Software Identification
        c     Remote Source Inclusion
        d     WebService
        e     Administrative Console
        x     Reverse Tuning Options (i.e., include all except specified)

To add them we use the `-Tuning` switch. So, in sum this command can look like this:

	nikto -o report.html -Format htm -Tuning 123bde -host <ip_addr>

Check [Nikto](https://tools.kali.org/information-gathering/nikto)'s own page for more information.

# Gobuster
Gobuster doesn't come built-in with Kali yet. To get it we use an apt-get command:

	sudo apt-get install gobuster

Gobuster is a directory enumeration tool, akin to `dirb` and `dirbuster` but I find it much more quicker and informative. To use it we only need to run it via

	gobuster -u <ip_address> -w <path_to_wordlist>

I usually use wordlists coming with Kali linux, but we can use any wordlist here.


# Final words
With nmap, we check the open ports and enumerate the applications running on them, allowing us to do more with metasploit ;)
With nikto, we do an initial scan on the webapp running on the found webserver, if there are any
With gobuster, we check the folder structure on the webserver with a predefined wordlist. 

Thank you for reading m8s!
