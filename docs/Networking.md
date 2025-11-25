# Networking Overview

This document describes the network design for the mini-enterprise-network. It explains the architecture, the reasoning behind design choices, and how VirtualBox, pfSense and the VMs networking layers interact to form a safe, isolated environment. The goal is to create a enterprise-like system.

## 1. Overview of the Network
- pfSense works as router + firewall
- A simulated WAN network (no real internet access)
- An isolated LAN network
- Three VMs:
    - Windows (workstation)
    - Ubuntu(Server/workstation)
    - Kali (attacker VM)

## 2. Architecture reasoning

### pfSense needs two NICs
- As a firewall/router pfSense needs both a WAN interface and a LAN interface

### WAN uses Host-Only:
- Creates a safe "internet"
- Isolated
- Host can access pfSense if needed (debugging etc)
- No real internet exposure

### LAN uses Internal Network
- All VMs communicate through pfSense
- They are all isolated from host PC

### NAT used during installation
- NAT was needed for reliable installation of pfSense and Windows VM which wasn't installed previously. 
- After installation NAT was removed to enforce isolation and safety.

## 3. Final Network Design & Justification

### WAN Network 10.0.0.0/24
- VirtualBox: Host-only adapter
- pfSense WAN: 10.0.0.1
- Fake Gateway: 10.0.0.254
- Purpose: Simulate ISP / upstream network

### LAN Network 192.168.10.0/24
- VirtualBox Internal Network(LAN-NET)
- pfSense LAN: 192.168.10.1
- All VMs only connected here

## 4. IP Address Plan

| Device      | IP Address    | Network       | Purpose                  |
| ----------- | ------------- | ------------- | ------------------------ |
| pfSense WAN | 10.0.0.1      | Host-Only WAN | Upstream interface       |
| WAN Gateway | 10.0.0.254    | Host-Only WAN | Fake ISP gateway         |
| pfSense LAN | 192.168.10.1  | Internal LAN  | LAN gateway              |
| Windows VM  | 192.168.10.10 | Internal LAN  | Windows orkstation       |
| Ubuntu VM   | 192.168.10.20 | Internal LAN  | Linux workstation/Server |
| Kali VM     | 192.168.10.30 | Internal LAN  | Attacker machine         |


### VM IPs
- All VM IPs were static to keep predictable, easy documentation and management.

## 5. Routing Logic
All traffic goes through pfSense:

### LAN -> pfSense -> WAN
- Each VM sends traffic to pfSense LAN (192.168.10.1)
- pfSense routes and NAT to WAN
- WAN has no external internet making it safe

### WAN -> pfSense -> LAN
- Blocked by default 

## 6. Security Benefits

### Host PC protected
- Internal Network prevents any VM from touching host

### No internet exposure
- Host-Only WAN removes risk of:
    - accidental port scanning
    - malware reaching the real internet
    - violating policies

### Centralized traffic inspection
- All traffic passes through pfSense, allowing:
    - packet capture
    - firewall rule testing
    - IDS/IPS later

### Enterprise-like segmentation
- WAN (untrusted) -> Firewall -> LAN (trusted)


