![image](https://docs.netbox.dev/en/stable/netbox_logo.svg)

# The Premiere Network Source of Truth

NetBox is the source of truth for everything on your network, from physical components like power systems and cabling to virtual assets like IP addresses and VLANs. Network automation and monitoring tools draw from this authoritative plan to push out configurations and monitor changes across the enterprise.

## Installation

1. On Proxmox, create a new container utilizing the latest Debian release
2. Update everything with `apt` and install `git`, `docker`, `docker-compose`, and `containerd`
    ```bash
	apt update && apt upgrade -y; apt autoclean -y; apt autoremove -y; apt install -y git docker docker-compose containerd
	```
3. Copy and paste the following into the terminal. While you wait for it to build and boot, update your firewall rules.
    ```bash
	git clone -b release https://github.com/netbox-community/netbox-docker.git
	cd netbox-docker
	tee docker-compose.override.yml <<EOF
	version: '3.4'
	services:
    netbox:
      ports:
        - 8000:8080
	EOF
	docker-compose pull
	docker-compose up
	```

4. Create your user to log in:
   ```bash
   docker-compose exec netbox /opt/netbox/netbox/manage.py createsuperuser
   ```
5. The whole application will be available after a few minutes. Open the URL ```http://0.0.0.0:8000/``` in a web-browser. You should see the NetBox homepage.