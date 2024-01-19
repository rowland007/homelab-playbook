# Installing AC-Hunter on Proxmox

![image](https://www.activecountermeasures.com/wp-content/uploads/2022/12/COMMUNITY-EDITION-BOX.png)

## RTFM First

- [Preinstall Guide](https://www.activecountermeasures.com/wp-content/uploads/2023/02/AC-Hunter-Pre-Install-Guide-v6_3_0-CE.pdf)
- [Install Guide](https://www.activecountermeasures.com/wp-content/uploads/2023/06/AC-Hunter-Install-Guide-v6_3_0-CE_v2.pdf)

## The Procedure

!!! note
    This process will install Zeek, BeaKer, and AC-Hunter.

1. Install Proxmox (this guide does not cover how to do that)
2. Navigate to Proxmox's CT Templates and download `ubuntu-20.04-standard_20.04-1_amd64.tar.gz`
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
6. Create a new CT with
   ```
   VM ID: <as applicable>
   Name: <zeek or whatever seems appropriate>
   Disk: 500GB
   CPU: 4 Cores
   RAM: 16GB (16384MB)
   Swap: 16GB (16384MB)
   Network: <appropriate Bridge> (this will be management)
   ```
7. Open the new VM settings and attach the vmbr as a *second* network interface and UNCHECK firewall
8. Create a new CT with
   ```
   VM ID: <as applicable>
   Name: <ACHunter or whatever seems appropriate>
   Disk: 500GB
   CPU: 4 Cores
   RAM: 16GB (16384MB)
   Swap: 16GB (16384MB)
   Network: <appropriate Bridge> (this will be management)
   ```
9. Start the AC-Hunter and Zeek CTs
10. Update both systems
11. Setup SSH for them to communicate. Apply the following commands to each container. Add them to the `/etc/hosts` file, and then use `ssh-copy-id` to each other's servers including itself.
12. In the Proxmox shell  
   In the commands below, the `ip link | grep ovs-system` command will show all the interfaces, you're looking for a `ovs-system` with the VM's ID in the interface. For example, if you have the Zeek container as VM 201, you'd look for `veth201i1`. You will replace that in the second command. You will also replace the # with the vmbr you created earlier
   ```
   root@pve:~# ip link
   root@pve:~# ovs-vsctl --id=@p get port veth<VMID>i1 -- --id=@m create mirror name=span1 select-all=true output-port=@p -- set bridge vmbr# mirrors=@m
   ```
   !!! warning 
       Do not include the @if# after the interface.  
13. [Download](https://www.activecountermeasures.com/ac-hunter-community-edition/linux-download/) the AC-Hunter *tar* file into the AC-Hunter container
14. Run the install script based on the *Install Guide* (see, told you to RTFM.)
    ```
    tar xvf *.tar
    cd achunter
    ./install_acm.sh zeek root@zeek achunter root@achunter beaker root@achunter
    ```