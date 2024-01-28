# Installing Security Onion on Proxmox

![image](https://securityonionsolutions.com/img/graphics/peelback-half.jpg
)

!!! note
    I am running this on my home network to experiment with Security Onion. See the link down below about the warning about running capturing packets in a VM.

1. Install Proxmox (this guide does not cover how to do that)
2. [:octicons-link-external-16: Download](https://github.com/Security-Onion-Solutions/securityonion/blob/2.4/main/DOWNLOAD_AND_VERIFY_ISO.md) the Security Onion ISO to Proxmox
3. Install OpenV Switch in Proxmox
   ```
   root@pve:~#  apt install -y openvswitch-switch
   ```
4. Create an OVS vmbr and port  
   a. In the Proxmox Network, create a new OVS Bridge and give it a vmbr name and ensure `Autostart` is selected  
   b. In the Bridge ports section, select the physical interface ie. `eno4`
5. In a Proxmox shell (replace the # with your vmbr name)
   ```
   root@pve:~# ovs-vsctl clear bridge vmbr# mirrors
   ```
6. Create a new VM with
   ```
   VM ID: <as applicable>
   Name: <SecOnion or whatever seems appropriate>
   Disk: 500GB
   CPU: 2 Sockets / 2 Cores
   RAM: 16GB (16384MB)
   Network: <appropriate Bridge> (this will be management)
   ```
7. Open the new VM settings and attach the vmbr as a second network interface and UNCHECK firewall
8. Start the VM and install Security Onion as a standalone
9. In the Proxmox shell  
   In the commands below, the `ip link` command will show all the interfaces, you're looking for a `tap` followed by the VM's ID. For example, if you have Security Onion as VM 101, you'd look for `tap101i1`. You will replace that in the second command. You will also replace the # with the vmbr you created earlier
   ```
   root@pve:~# ip link
   root@pve:~# ovs-vsctl --id=@p get port tap<VMID>i1 -- --id=@m create mirror name=span1 select-all=true output-port=@p -- set bridge vmbr# mirrors=@m
   ```
   
## Resources/Sources

- [:octicons-link-external-16: Installing Security Onion on Proxmox video](https://www.youtube.com/watch?v=BA6wuWM9acY) :simple-youtube:
- [:octicons-link-external-16: Security Onion and Proxmox FYI on promisc setup](https://github.com/Security-Onion-Solutions/securityonion/discussions/8245) :simple-github:
- [:octicons-link-external-16: HoldMyBeer Security: Install/Setup Zeek + PF_Ring on Ubuntu 18.04 on Proxmox 5.3 + OpenVSwitch](https://holdmybeersecurity.com/2019/04/03/part-1-install-setup-zeek-pf_ring-on-ubuntu-18-04-on-proxmox-5-3-openvswitch/) :fontawesome-solid-blog:
- [:octicons-link-external-16: Active Countermeasures: Is It OK to Capture Packets in a Virtual Machine?](https://www.activecountermeasures.com/is-it-ok-to-capture-packets-in-a-virtual-machine/) :fontawesome-solid-blog:
