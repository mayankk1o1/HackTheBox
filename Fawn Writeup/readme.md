## Overview

Fawn is a beginner-friendly Hack The Box machine that introduces the basics of network enumeration and FTP misconfigurations.

The machine started with an Nmap scan to identify open ports and running services. During enumeration, port 21 was found open, indicating that an FTP service was running on the target machine.

Further investigation revealed that the FTP server allowed anonymous login. Using the FTP client, access was gained without requiring any valid credentials.

FTP Login Command:

`ftp <target-ip>`

Anonymous Login:

`Username: anonymous`

After successfully logging in, directory enumeration was performed and a file containing the flag was discovered. The flag was then retrieved directly from the FTP server.

## Key Learnings

* Basic network enumeration using Nmap
* Identifying FTP services on port 21
* Understanding anonymous FTP login
* Enumerating files through FTP access
* Retrieving sensitive information from misconfigured services

## Skills Practiced

* Service Enumeration
* FTP Enumeration
* Anonymous Authentication Testing
* Basic Linux Navigation
* Information Gathering

Fawn is an excellent starter machine for understanding how insecure service configurations, such as anonymous FTP access, can expose sensitive data to attackers.
