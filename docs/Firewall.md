# Firewall Rules & Order

## ADMIN-NET
Only default allow all outbound communication from ADMIN-NET. Allow full access for control. 
## Technical Rule
Interface: LAN
Action: Allow
Address Family: IPv4 + IPv6
Protocol: Any
Source: 192.168.10.0/24
Destination: *
Destination Port: Any
Logging: Disabled
Description: 
Rule Position: 

## Windows-NET

### Order
1. Allow Windows DNS -> pfSense
## Technical Rule
Interface: LAN
Action: Allow
Protocol: TCP
Source: 192.168.20.100
Destination: 192.168.20.1
Destination Port: 53(DNS)
Logging: Enabled
Description: Allow DNS access from Windows for internet access.
Rule Position: #1
2. Block Windows -> pfSense(firewall)
## Technical Rule
Interface: LAN
Action: Block
Protocol: Any
Source: 192.168.20.100
Destination: 10.0.0.0/24
Destination Port: Any
Logging: Enabled
Description: Block access from Windows to pfSense firewall.
Rule Position: #2
3. Block Windows -> Kali
## Technical Rule
Interface: LAN
Action: Block
Protocol: Any
Source: 192.168.20.100
Destination: 192.168.30.10
Destination Port: Any
Logging: Enabled
Description: Block access to Kali-NET from Windows.
Rule Position: #3
4. Block Windows -> ADMIN-NET
## Technical Rule
Interface: LAN
Action: Block
Protocol: Any
Source: 192.168.20.100
Destination: 192.168.10.0/24
Destination Port: Any
Logging: Enabled
Description: Block access to ADMIN-LAN for Windows workspace
Rule Position: #4
5. Allow outbound traffic
## Technical Rule
Interface: LAN
Action: Allow
Protocol: Any
Source: 192.168.20.100
Destination: *
Destination Port: Any
Logging: Disabled
Description: Allow all outbound traffic from Windows
Rule Position: Bottom


## Kali-NET
1. Allow Kali -> Firewall DNS
## Technical Rule
Interface: LAN
Action: Block
Protocol: TCP/UDP
Source: 192.168.30.10
Destination: 192.168.30.1
Destination Port: 53(DNS)
Logging: Disabled
Description: 
Rule Position: 
2. Block Kali -> Firewall
## Technical Rule
Interface: LAN
Action: Block
Protocol: Any
Source: 192.168.30.100
Destination: 192.168.30.1
Destination Port: Any
Logging: Enabled
Description: Block traffic Kali -> Firewall
Rule Position: #2

3. Block Kali -> ADMIN-NET
## Technical Rule
Interface: LAN
Action: Block
Protocol: Any
Source: 192.168.30.10
Destination: 192.168.10.0/24
Destination Port: Any
Logging: Enabled
Description: Block traffic Kali -> ADMIN-NET (Ubuntu + pfSense)
Rule Position: #3
4. Block Kali -> Windows
## Technical Rule
Interface: LAN
Action: Block
Protocol: Any
Source: 192.168.30.10
Destination: 192.168.20.0/24
Destination Port: Any
Logging: Enabled
Description: Block traffic Kali -> Windows-NET
Rule Position: #4
5. Allow outbound traffic Kali
## Technical Rule
Interface: LAN
Action: Allow
Protocol: Any
Source: 192.168.30.10
Destination: *
Destination Port: Any
Logging: Enabled
Description: Enable outbound access from Kali 
Rule Position: #5, 

## Technical Rule
Interface: LAN
Action: Block
Protocol: Any
Source: 192.168.10.0/24
Destination: 10.0.0.0/24
Destination Port: Any
Logging: Enabled
Description: 
Rule Position: 