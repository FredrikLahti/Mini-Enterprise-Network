# Firewall Tests

##ADMIN

### Default full access
ping each VM and 8.8.8.8
Predicition: all work
Actually: all work


## Windows rules
Should be able to access internet but none of the VMs except DNS to pfSense
Predicition: Nothing works except internet access
Actually: All pings failed except to 8.8.8.8 -> Success

## Kali Rules
All VMs and firewall should have Kali blocked. Only internetaccess through port 53
Prediction: Nothing works except internet access
Actually: All pings failed except 8.8.8.8 -> Success
