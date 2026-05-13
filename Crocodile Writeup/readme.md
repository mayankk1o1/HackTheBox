Crocodile is a beginner-friendly Linux machine on Hack The Box that focuses on FTP enumeration, anonymous login access, credential discovery, directory brute-forcing, and basic web authentication testing.

The machine started with an Nmap scan to identify open ports and running services:

```bash
nmap -sC -sV <IP>
```
![alt text](<Screenshot 2026-05-13 232158.png>)


The scan revealed two important services:

- Port `21` running **vsftpd 3.0.3**
- Port `80` running **Apache httpd 2.4.41**

Anonymous FTP login was enabled, which allowed access to downloadable files hosted on the server.

```bash
ftp <IP>
```

While connecting to the FTP server, the username `anonymous` was used to log in successfully.

```bash
Name: anonymous
```

After logging in, the available files were listed:

```bash
ls
```

Two interesting files were discovered:

```text
allowed.userlist
allowed.userlist.passwd
```


The files were downloaded using the `get` command:

```bash
get allowed.userlist
get allowed.userlist.passwd
```

![alt text](<Screenshot 2026-05-13 231838.png>)



The downloaded files contained usernames and passwords that could potentially be used for authentication.


# Web Enumeration

After identifying the Apache web server on port `80`, directory brute-forcing was performed using Gobuster to discover hidden files and directories.

```bash
gobuster dir -u http://<IP> -w /usr/share/SecLists/Discovery/Web-Content/big.txt -x php
```

The scan revealed a login page:

```text
/login.php
```

This page provided the opportunity to authenticate to the web application using the previously discovered credentials.

---

# Authentication

Using the credentials gathered from the FTP files, authentication to the web application was successful and access to the dashboard was obtained.

After logging in, the root flag was successfully captured.

---

# Key Learnings

- Performing reconnaissance using Nmap
- Enumerating FTP services
- Understanding anonymous FTP access risks
- Downloading files from FTP servers
- Discovering sensitive credential files
- Directory brute-forcing using Gobuster
- Identifying authentication portals
- Basic credential-based authentication testing
- Web application enumeration methodology

---

# Skills Practiced

- Linux Enumeration
- FTP Enumeration
- Anonymous FTP Exploitation
- Credential Discovery
- Gobuster Directory Enumeration
- Web Application Reconnaissance
- Authentication Testing

---

