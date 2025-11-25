# Host System Documentation

This document describes the physical host machine and virtualization environment used to run the project.
It provides hardware details, virtualization configuration, and resource planning for all virtual machines

## 1. Host Machine Overview

**Host Operating System:**  
<Windows 11 Home 23H2>

**CPU / Processor:**  
<Intel Core i7-13700F — 16 cores / 24 threads>

**Memory (RAM):**  
<16 GB DDR4>

**Storage:**  
<1 TB SATA SSD>

**Virtualization Support:**  
- Virtualization enabled in BIOS: <Yes>  
- Technology: <Intel VT-x>

**Notes:**  
<Desktop system. Adequate thermal headroom.>

## 2. Virtualization Software
**Hypervisor:**  
<Oracle VirtualBox>

**Reason for Choice:**  
- <free, well known>

**Version:**  
<7.2.4>

## 3. Resource Allocation Plan

This section defines how the host's resources will be distributed across the lab's VMs

### pfSense Router/Firewall
- vCPUs: <1–2>  
- RAM: <1 GB>  
- Storage: <8–10 GB>  
- Network Adapters:  
  - WAN → `10.0.0.0/24` network  
  - LAN → `192.168.10.0/24` network

### Windows 10 Client VM
- vCPUs: <2> 
- RAM: <4 GB>  
- Storage: <40-60 GB>  
- Network Adapters: LAN

### Ubuntu Server VM
- vCPUs: <1-2> 
- RAM: <2 GB>  
- Storage: <20-40 GB>  
- Network Adapters: LAN

### Kali attacker VM
- vCPUs: <1-2>
- RAM: <4GB>
- Storage: <80GB>
- Network Adapters: LAN

***Total planned resource usage:***
CPU usage: <5-7>
RAM usage: <11 GB>
Storage: <148-190 GB>
***Expected remaining for host:*** 
vCPU: <8-10>
RAM: <5 GB>
Storage: <810 GB>

## 4. Virtual Network Planning

Two isolated virtual networks will be created in Virtualbox

### WAN Network (Simulated internet)
- Network type: <Internal Network / Host-only>
- Subnet: `10.0.0.0/24`
- Purpose: Safe, isolated "internet" connection for pfSense WAN

### LAN Network (Internal Corporate Network)
- Network type: Internal Network
- Subnet: `192.168.10.0/24`
- Purpose: Windows + Ubuntu internal communication through pfSense

## 5. Screenshots
Screenshots for host-system is located under `/screenshots/host-system/`




