# Network setup and segmentation

Previously all VM's were setup in the same LAN making it possible to communicate directly even though I had set pfSense as gateway. To defend against this i'm now segmenting each VM into its own subnet.

## How to set up subnets

1. I will first have to add more NICs to pfSense for each new subnet.
    It's very important to set a unique name for each subnet.
2. I'll then assign them inside pfSense so the name makes sense but also to give each interface an IP
    I will have DHCP disabled so that my network diagram stays valid and also so nothing changes all the sudden.
3. I'll then attach each VM to its corresponding LAN-NET inside VirtualBox
4. This should do so that when my VMs try to communicate they will be forced to go through pfSense, even for ICMP etc. 
