# Summary of Issue and Resolution

The connectivity failure between Ubuntu and pfSense was caused by a mismatch between VirtualBox adapter numbers and pfSense interface assignments. Although both pfSense and Ubuntu used an internal network named “Admin-LAN,” they were connected to different physical virtual NICs inside pfSense. pfSense had LAN assigned to *em1*, but “Admin-LAN” was physically connected to *Adapter 2*, which maps to *em0*. Ubuntu was also connected to Adapter 2, so it attempted to reach pfSense on em0 while pfSense was listening for LAN traffic on em1. This resulted in ARP failures, inability to ping, and inability to access the pfSense GUI.

During debugging, multiple potential causes were tested and eliminated, including DNS issues, firewalls, routing tables, upstream gateway configuration, and network naming inconsistencies. Interface status was checked, IPs were reassigned, and Ubuntu’s static configuration was updated after moving its adapter. Ping continued to fail, indicating the underlying issue was not IP configuration but physical NIC mismatch inside the VM.

## The root cause was identified by comparing MAC addresses between VirtualBox and pfSense. This confirmed that:

* pfSense Adapter 2 (the internal Admin-LAN network) corresponded to *em0*, not *em1*.
* Ubuntu was connected to Adapter 2 (correct), but pfSense had LAN assigned to *em1* (incorrect).
* As a result, Ubuntu and pfSense were plugged into different NICs even though they appeared to share the same internal network name.

## The final solution was to reassign pfSense interfaces to match the actual VirtualBox adapter layout:

* WAN → em1
* LAN → em0
* OPT1/OPT2 → remaining NICs

After reassigning LAN to em0 and reapplying the LAN IP configuration, Ubuntu was able to reach pfSense immediately. Connectivity, ARP, ping, and GUI access all functioned as expected.

The key lesson is that VirtualBox “Adapter 1/2/3/4” do not automatically match pfSense “em0/em1/em2/em3”; MAC address matching must be used to determine which pfSense interface corresponds to which VirtualBox adapter. Ensuring that both pfSense and a client VM use the same adapter number and internal network is critical for proper connectivity.
