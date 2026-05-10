## Overview

Dancing is a beginner-friendly Windows machine on Hack The Box that focuses on SMB enumeration and anonymous share access.

The machine started with a basic Nmap scan, which revealed SMB services running on ports `139` and `445`. Since SMB was exposed, the next step was to enumerate available shares using `smbclient`.

Install the sbmclient using this command - 
sudo apt-get install smbclient 


Shares were listed anonymously with:

```bash
smbclient -L //<IP>/ -N
```

During enumeration, a share named `WorkShares` was discovered. Interestingly, the share allowed anonymous access, meaning no username or password was required to connect. Hit enter and you will get the smb shell access - 

Access to the share was obtained using:

```bash
smbclient //<IP>/WorkShares
```

Inside the share, multiple user directories were found. After navigating through the folders, a `flag.txt` file was discovered and downloaded using the `get` command.

This machine highlights a very common real-world issue where improperly configured SMB shares expose sensitive files to unauthenticated users.

---

## Key Learnings

- Performing SMB enumeration with Nmap
- Understanding SMB shares and anonymous access
- Using `smbclient` for SMB interaction
- Enumerating directories and files inside shares
- Identifying insecure SMB configurations
- Downloading files from exposed shares

---

## Skills Practiced

- SMB Enumeration
- Windows Reconnaissance
- Network Share Analysis
- File Share Exploitation
- Post-Enumeration Navigation
- Basic Penetration Testing Methodology

Dancing is an excellent machine for beginners who want to understand how SMB enumeration works and how small misconfigurations in Windows file sharing can lead to sensitive information disclosure.