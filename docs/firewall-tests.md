# Firewall-tests 

This document is made to document firewall tests for the project.

## Rule 1 Allow Ubuntu -> pfSense

Goal: Ubuntu should access pfSense via HTTPS (443) and SSH (22)

### Test 1 - HTTPS
Command (Ubuntu): curl -I https://192.168.10.1
Expected: Connection succeeds
Actual: Connection succeeds.
Screenshots: /screenshots/firewall/FirewallRules/Rule1_Success

### Test 2 - SSH
Command: ssh admin@192.168.10.1
Expected: Prompt appears
Actual:
Screenshots:

## Rule 2 Allow Kali Test Ports
Goal: Kali can reach specific ports only

### Test 1 - Nmap scan for 445
Command: nmap -p 445 192.168.10.x
Expected: Port is open
Actual:
Screenshot:
pfSense logs:

## Rule 3 - Block Kali -> LAN
Goal: Anything not explicitly allowed is blocked

### Test 1 - Ping Windows
Command: ping 192.168.10.10
Expected: No replies
Actual:
Screenshot:
pfSense logs:

## Rule 4 - Block LAN -> WAN
Goal: LAN cannot contact WAN subnet

### Test Windows/Ubuntu
Command: ping 10.0.0.254
Expected: No replies
Actual:
Screenshot:
pfSense logs:

## Rule 5 - Allow LAN -> LAN
Command: ping 192.168.10.20
Expected: Replies
Actual:
Screenshot:

