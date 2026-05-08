# HTB - Meow

## Introduction

Meow is one of the very first and easiest machines you might encounter while starting your journey on :contentReference[oaicite:0]{index=0}.  

This machine introduces beginners to:
- Basic networking
- Open ports
- Telnet service
- Enumeration using Nmap
- Remote access concepts

---

# Initial Setup

Start the machine from the HTB website and connect to the VPN.

While setting things up, I found it a little confusing between a normal VPN and OpenVPN, so I spent some time understanding the difference.

## OpenVPN vs Normal VPN

### OpenVPN
OpenVPN is used to access the private network of a particular organization.

For example:
Here, we use OpenVPN to connect to the HTB lab environment so we can access their machines privately.

### Normal VPN
A normal VPN is usually used to:
- Hide your identity on the internet
- Mask your real IP address
- Access geo-restricted content

So in short:
- OpenVPN = Access a private network
- Normal VPN = Privacy and anonymity on the internet

---

# Machine Enumeration

After connecting to the VPN and starting the machine, HTB gives some beginner questions to solve.

The questions were fairly easy, but the real challenge started when it came time to submit the final flag.

---

# Step 1 - Check if the Machine is Alive

Open the terminal and run:

```bash
ping <IP>
```

This helps us confirm:
- The machine is running
- The host is reachable
- The target is responding

---

# Step 2 - Scan Open Ports Using Nmap

Nmap stands for **Network Mapper** and is one of the most important tools in cybersecurity for scanning open ports and detecting services.

Run:

```bash
nmap -sV <IP>
```

### Explanation
- `-sV` → Detects the version of the running services

After the scan completes, we find:

```bash
23/tcp open  telnet
```

![alt text](<Screenshot 2026-05-08 172430.png>)

This tells us that:
- Port 23 is open
- The Telnet service is running

---

# Understanding Telnet

Telnet is a protocol used to remotely access and manage another host over a network.

Usually, Telnet services require:
- Username
- Password

---

# Step 3 - Connect Using Telnet

Run:

```bash
telnet <IP>
```

This attempts to connect to the target machine.

Now things get interesting.

The service asks for a username and password.

At this stage, I tried some basic hit-and-trial methods with common usernames.

Eventually, access was granted to the Ubuntu machine.

---

# Step 4 - Find the Flag

Once logged in, run:

```bash
ls
```

This lists the files in the current directory.

Here, the flag file can be found and submitted on the HTB platform.

![alt text](<Screenshot 2026-05-08 175352.png>)

---

# What I Learned

- Difference between OpenVPN and normal VPN
- Basic machine enumeration
- Using `ping` to verify connectivity
- Scanning ports using Nmap
- Understanding open ports and services
- Basics of the Telnet protocol
- Remote access concepts
- Importance of enumeration in penetration testing

---

# Tools Used

- Ping
- Nmap
- Telnet

---

# Commands Used

```bash
ping <IP>

nmap -sV <IP>

telnet <IP>

ls
```

---

# Final Thoughts

Meow is a great beginner-friendly machine that teaches the importance of:
- Enumeration
- Service identification
- Understanding network protocols

A very simple but solid introduction to the HTB platform and practical cybersecurity learning.