# Mini Enterprise Network Lab
This file documents the core components of the project and how they interact.
It provides a high-level overview.

## 1. Overview

This lab simulates a small corporate network using virtual machines
It includes routing, firewalling, Windows and Linux systems, logging, user management, and basic security controls

### 2. Components

### pfSense Router/Firewall
- Acts as the network gateway
- Provides LAN/WAN separation
- Handles DHCP, NAT, firewall rules
- Logs traffic events
- Enforces network security policy

### Windows 10 Client
- Represents an employee workstation
- Used for:
    - connetivity testing
    - RDP/SSH usage
    - log inspection
    - interacting with Linux server
- Controlled via local Windows security policies

### Ubuntu Server
- Hosts internal services
- SSH server
- User and group management
- Permissions & directory structure
- UFW firewall enabled
- Fail2ban for SSH hardening
- Systemd services for background tasks

## 3. Network structure (high level)

**LAN Subnet:**
`192.168.10.0/24`
Windows + Linux VMs live here

**WAN Subnet:**
`10.0.0.0/24`
pfSense WAN side + simulated internet

**Routing:**
pfSense routes traffic between LAN -> WAN and performs NAT.

## 4. Security Controls
- pfSense firewall rules
- UFW on Limux
- Fail2ban for SSH brute-force prevention
- Strong password policy (Windows + Linux)
- Least Privilege user accounts

## 5. Goals of the architecture

- Demonstrate understanding of OS fundamentals
- Show basic enterprise network design skills
- Practice Windows/Linux admin tasks
- Practice implementation of firewalls and segmentation
- Generate logs for future SIEM/IDS expansion

