##  Task 1: Network Reconnaissance with Nmap

###  Objective  
Discover open ports on local devices to understand network exposure using Nmap.

###  Tools Used
- Kali Linux
- Metasploitable2 (Target)
- Nmap
- netdiscover

###  Steps Performed

1. Identified the IP address of the Metasploitable machine using:
   - `netdiscover` on Kali Linux
   - `ifconfig` inside the Metasploitable VM
2. Conducted a TCP SYN scan using:
   ```bash
   sudo nmap -sS 192.168.1.13 -oN metasploitable-scan.txt
3. Saved scan results to metasploitable-scan.txt
4. Analyzed open ports and assessed associated risks
5. Captured and documented supporting screenshots
## Screenshots

| Figure | Description                                           | Screenshot |
|--------|-------------------------------------------------------|------------|
| 1      | Launching `netdiscover` from Kali                     | ![Figure 1](screenshots/figure1_netdiscover_launch.png) |
| 2      | `netdiscover` reveals Metasploitable IP               | ![Figure 2](screenshots/figure2_netdiscover_ip.png)     |
| 3      | Confirming IP address from inside Metasploitable      | ![Figure 3](screenshots/figure3_ifconfig_metasploitable.png) |
| 4      | Nmap scan being performed from Kali                   | ![Figure 4](screenshots/figure4_nmap_scan.png)          |
| 5      | Viewing saved scan result file using `cat`            | ![Figure 5](screenshots/figure5_cat_scan_result.png)    |


## Nmap Scan Result Summary

- **Target IP:** `192.168.1.13`  
- **Scan Time:** 0.32 seconds  
- **Command Used:**
  ```bash
  nmap -sS 192.168.1.13 -oN metasploitable-scan.txt
Key Open Ports and Services:
> | Port  | State | Service     | Risk Notes                            |
> |-------|-------|-------------|----------------------------------------|
> | 21    | open  | ftp         | May allow anonymous login              |
> | 22    | open  | ssh         | Secure shell (check weak credentials)  |
> | 23    | open  | telnet      | Unencrypted, insecure                  |
> | 25   | Open   | SMTP          | Could be abused for spam       |
> | 53   | Open   | DNS           | Domain Name System             |
> | 80   | Open   | HTTP          | Web server                     |
> | 111  | Open   | RPCBind       | Common in exploits             |
> | 139  | Open   | NetBIOS-SSN   | Windows file sharing           |
> | 445   | open  | microsoft-ds  | SMB; vulnerable to EternalBlue                  |
> | 512   | open  | exec          | Legacy service; insecure                        |
> | 513   | open  | login         | Unencrypted remote login                        |
> | 514   | open  | shell         | Remote shell access                             |
> | 1099  | open  | rmiregistry   | Java RMI; vulnerable in older setups            |
> | 1524  | open  | ingreslock    | Often used by backdoors                         |
> | 2049  | open  | nfs           | File access risk                                |
> | 3306  | open  | mysql         | Weak root login could be exploitable            |
> | 5432  | open  | postgresql    | Database service                                |
> | 5900  | open  | vnc           | Unsecured remote desktop                        |
> | 6000  | open  | X11           | Graphical interface exposed                     |
> | 6667  | open  | irc           | Botnet control channel possible                 |
> | 8009  | open  | ajp13         | Apache JServ; test for Ghostcat exploit         |
> | 8180  | open  | http-alt      | Alternate web service                           |




##  Observations & Risk Summary

- Multiple high-risk services are running, including **Telnet**, **SMB**, and **RMI**.
- Remote access ports such as **VNC (5900)**, **X11 (6000)**, and **SSH (22)** are open, which can be potential entry points for attackers.
- The **SMB** service (port 445) is exposed, which is commonly exploited using tools like **EternalBlue**.
- The overall configuration and exposed services strongly suggest this is a **deliberately vulnerable machine** (e.g., Metasploitable).

---

##  Learnings

- Used `netdiscover` and `ifconfig` to locate and confirm the target IP address on the network.
- Performed a **stealth TCP SYN scan** using `nmap` to avoid detection while enumerating open ports.
- Analyzed discovered services to **identify real-world vulnerabilities** and assess exploitation potential.
- Practiced **documenting results** and compiling them into a **security-focused report** for analysis and presentation.


