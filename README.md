# IT-Infrastructure-Lab

## Project Summary

This project simulates a real-world internal IT network infrastructure using VirtualBox, Ubuntu Server, and multiple Ubuntu client VMs. It integrates core IT services including DNS, DHCP, Samba file sharing, and a web-based help desk system (GLPI). The project is organized into phases and includes automation scripts, documentation, and a clean folder structure to reflect enterprise-level planning and implementation.

---

## Tech Stack

| Component      | Purpose                                       |
| -------------- | --------------------------------------------- |
| VirtualBox     | Virtualization platform                       |
| Ubuntu Server  | Infrastructure services (DNS, DHCP, Samba)    |
| Ubuntu Desktop | Simulated client machines                     |
| Host-Only Net  | Internal LAN-style networking (vboxnet0)      |
| BIND9          | DNS server for internal name resolution       |
| ISC DHCP       | IP address assignment to clients              |
| Samba          | Shared folder for file access                 |
| Apache + PHP   | Web server for GLPI                           |
| MariaDB        | Backend database for GLPI                     |
| GLPI           | Web-based IT ticket/help desk system          |
| Bash           | Custom automation scripts                     |
| Git & GitHub   | Documentation and version control             |

---

##  Setup Instructions

### Virtual Machine Setup
1. **Install VirtualBox**
2. **Create VMs:**
   - `IT-Server`: Ubuntu Server
   - `Client-01`: Ubuntu Desktop
   - `Client-02`: Ubuntu Desktop
3. **Networking:**
   - Configure **Host-Only Adapter** (`vboxnet0`)
   - Ensure all VMs are in the same internal LAN

###  Core Network Services
4. **DNS Setup:**
   - Install `bind9` on IT-Server
   - Configure forward zone: `ns1.internal.lan`
   - Test DNS resolution from clients

5. **DHCP Setup:**
   - Static IP for Client-01
   - Dynamic IP via DHCP for Client-02

6. **Samba Shared Folder:**
   - Guest-access shared directory setup on server
   - Accessible from both client machines

###  Help Desk System (GLPI)
7. **Web Server Stack:**
   - Install Apache, PHP 8.3, and MariaDB
   - Create GLPI database and user
   - Install and configure GLPI 10.0.15
   - Test access at: `http://ns1.internal.lan`

8. **Post-Install Security:**
   - Remove `/install` directory

###  Scripting & Automation
9. **Bash Script:**
   - `ping-check.sh`: Verifies network connectivity

---

## 🛠️ Features & Tasks Completed

### Week 1–2: VirtualBox & VM Setup
- VirtualBox + Extension Pack installed
- Ubuntu Server + 2 Ubuntu Desktop VMs created
- Host-only networking (vboxnet0) configured
- Verified ping between clients and server

### Week 3–4: DNS, DHCP, Samba
- BIND9 installed and configured
- DNS zone created for `internal.lan`
- Clients configured using Netplan
- Samba guest-share accessible from clients

### Week 5–6: GLPI Help Desk
- Apache, PHP 8.3, MariaDB stack configured
- GLPI installed, configured, and tested
- Sample ticket (“Printer Offline”) successfully created

### Week 7–8: Scripting & Automation
- Bash scripts implemented and tested
- Hostname resolution verified via DNS
- ICMP reachability confirmed for all nodes

### Week 9–10: Documentation & Cleanup
- All `.txt` files converted to `.md`
- Main `README.md` created
- Repository cleaned and finalized

---

 Detailed step-by-step guides are available in subdirectories:
- Services
- Helpdesk
- Scripts

---

Zakary Rawles 
`https://github.com/zrawles2023`


