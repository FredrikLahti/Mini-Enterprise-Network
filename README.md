# Mini Enterprise Network Lab

A self-contained, virtualized enterprise network designed to practice foundational skills in the following areas:

- Operating Systems (Windows & Linux (Ubuntu))
- Networking(routing, NAT, firewalling)
- Security (permissions, hardening, logs)
- Virtualization(VMs and internal networks)
- Documentation & Project structure

This project simulates a small corporate environment with a router/firewall, a Windows workstation, and a Linux server. All contained and isolated inside a virtual network.

## Architecture Overview
![Network Diagram](architecture/network-diagram.png)
*(Diagram will be added when created)*

The project consists of three core virtual machines:

Component | Purpose

**pfSense Router/Firewall** | Gateway, NAT, segmentation, security policy
**Windows 10 Client** | Employee workstation, connectivity testing, event logs
**Ubuntu Server** | Internal server hosting SSH, logging, permissions, services

More details are available at:
[`architecture/components.md`](architecture/components.md)

## Learning Objectives

This project is created to increase competency in:

- Linux user management, file permissions & services
- Windows administration & security settings
- Network design (subnets, DHCP, routing, firewalling)
- NAT and traffic flow analysis
- Log analysis across pfSense, Linux, and Windows
- HArdening practices (SSH, firewall rules, fail2ban)
- "Real world"-style documentation
- Clean project structuring
- Working with VMs in a controlled lab environment

## Project Structure

mini-enterprise-network-lab/
|--architecture/
|--setup/
|--configuration/
|--testing/
|--logs/
|--screenshots/
|--README.md

See the `architecture/` directory for high-level design.
See the `setup/` for installation/configuration instructions

## Current Status

- [x] Project initialized  
- [x] Architecture folder created  
- [x] Components documented  
- [] Network diagram  
- [] pfSense installation  
- [] Windows VM installation  
- [] Ubuntu server installation  
- [] Configuration  
- [] Testing & validation  
- [] Documentation screenshots

## Project Roadmap

### **v1.0 Core Functionality**
- pfSense installed & configured
- LAN/WAN segmentation
- Windows + Ubuntu VMs setup
- SSH + UFW + fail2ban on Linux
- Basic Windows security configurations
- NAT + firewall rules implemented

### **v1.1 Security Expansion**
- Nmap scanning tests
- Log correlation between systems
- Failed login attempts analysis
- Hardening improvements

### **v1.2 Optional Expansions**
- Add Windows server + AD
- Add IDS/IPS (Suricata)
- Add Wazuh/Graylog SIEM
- Add vulnerable web apps + detection tests
- Add Linux distribution Kali as attack VM

## Screenshots

Screenshots will be added as the lab is built.
They will live under: `/screenshots/`
