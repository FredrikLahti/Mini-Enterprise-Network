# Rules Order

1. Allow Ubuntu → pfSense (management)
2. Allow Kali → Windows/Ubuntu (specific testing ports)
3. Block Kali → LAN (full isolation, logged)
4. Block LAN → WAN (logged)
5. Allow LAN → LAN (normal communication)
6. Allow LAN → Any (Default LAN rule)

# Rule 1 — Allow Ubuntu to Manage pfSense (HTTPS + SSH)

Since Ubuntu is my admin workstation, it needs controlled access to:
- pfSense Web UI (443)
- pfSense SSH (22)

This has to be highest priority so it’s never accidentally blocked.

## Technical Rule
Interface: LAN
Action: Allow
Protocol: TCP
Source: 192.168.10.20
Destination: 192.168.10.1
Destination Port: 443, 22
Logging: Enabled (for safety: note suspicious behavior)
Description: Allow Ubuntu admin workstation to manage pfSense (HTTPS/SSH)
Rule Position: Top (#1)

# Rule 2 — Allow Specific Kali Testing Ports (445, 3389, ICMP)

Kali is only allowed controlled, explicit testing on Windows/Ubuntu.

## Technical Rule
Interface: LAN
Action: Allow
Protocol: TCP, ICMP
Source: 192.168.10.30
Destination: 192.168.10.0/24
Destination Port: 445, 3389
Logging: Enabled
Description: Allow Kali to reach LAN workstations for controlled test ports
Rule Position: #2 (must be above general Kali block rule)

# Rule 3 — Block All Kali → LAN Communication (Logged)

The Kali machine should be isolated except when explicitly allowed.

## Technical Rule
Interface: LAN
Action: Block
Protocol: Any
Source: 192.168.10.30
Destination: 192.168.10.0/24
Destination Port: Any
Logging: Enabled
Description: Block all Kali -> LAN traffic to isolate VM
Rule Position: Below Rule 2 to allow explicit testing

# Rule 4 — Block LAN → WAN (Logged)

Since my WAN is a simulated ISP network, I’m blocking outbound LAN traffic to mimic enterprise egress filtering as a baseline.

## Technical Rule
Interface: LAN
Action: Block
Protocol: Any
Source: 192.168.10.0/24
Destination: 10.0.0.0/24
Destination Port: Any
Logging: Enabled
Description: Block LAN access to WAN (simulated upstream network)
Rule Position: #4 (below Kali block rule, above general allow LAN rule)

# Rule 5 — Allow Normal LAN → LAN Communication

Default internal communication should be allowed (ICMP, SMB, SSH, etc).
This is the base allowance.

## Technical Rule
Interface: LAN
Action: Allow
Protocol: Any
Source: 192.168.10.0/24
Destination: 192.168.10.0/24
Destination Port: Any
Logging: Disabled (too much noise)
Description: Baseline allowance in LAN internal communication
Rule Position: Near the bottom (#5)

# Rule 6 — pfSense Built-In Allow Rule

This is the pfSense default rule allowing LAN → Any.
I’ve decided to keep it for learning and debugging.

## Technical Rule
Interface: LAN
Action: Allow
Protocol: Any
Source: 192.168.10.0/24
Destination: Any
Destination Port: Any
Logging: Disabled
Description: Default LAN rule
Rule Position: Bottom (#6)

# Reasoning for Rule Order

This order guarantees:
- Ubuntu always has management access
- Kali is mostly isolated
- Kali can only do controlled tests
- LAN cannot reach WAN
- LAN can reach itself