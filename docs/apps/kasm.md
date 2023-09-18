![kasm-logo](https://www.kasmweb.com/docs/latest/_static/Kasm_Workspaces_Logo.svg)

## The Container Streaming Platform®

Streaming containerized apps and desktops to end-users. The Workspaces platform provides enterprise-class orchestration, data loss prevention, and web streaming technology to enable the delivery of containerized workloads to your browser.

## Installation Requirements

??? info "Source"
    [Kasm Docs](https://www.kasmweb.com/docs/latest/install/system_requirements.html#kasm-workspaces-requirements)

### Supported Operating Systems

- Ubuntu 18.04 / 20.04 / 22.04 (amd64/arm64)
- Debian 10 / 11 / 12 (amd64/arm64)
- CentOS 7 / 8 / 9 (amd64/arm64)
- Oracle Linux 7 / 8 / 9 (amd64/arm64)
- Raspberry Pi OS (Debian) 10 / 11 / 12 (arm64)
- [Other](https://www.kasmweb.com/docs/latest/how_to/other_operating_systems.html)

### Resource Requirements

- **CPU**: 2 Cores
- **Memory**: 4GB
- **Storage**: 50GB

!!! warning
    This is the minimum requirement to run the Kasm services and Agent. You will need more space to download additional workspaces. It is recommened to have more resources available for sessions

## Installation

??? info "Installation Guide"
    [Kasm Docs](https://www.kasmweb.com/docs/latest/install/single_server_install.html)

1. On Proxmox, create a new container utilizing the latest Debian release
2. Update everything with `apt` and install `curl`
    ```bash
	apt update && apt upgrade -y; apt autoclean -y; apt autoremove -y; apt install -y curl
	```
3. Copy and paste the following into the terminal. While you wait for it to build and boot, update your firewall rules.
    ```bash
    cd /tmp
    curl -O https://kasm-static-content.s3.amazonaws.com/kasm_release_1.14.0.3a7abb.tar.gz
    tar -xf kasm_release_1.14.0.3a7abb.tar.gz
    kasm_release/install.sh --accept-eula 
    ```
    !!! tip
        Check the documentation to get the latest release. They do not use a "latest" tag to download the tar.
    !!! danger
        The install will only show the passwords once. Ensure you get a screen capture of the passwords so you can log in.
4. The whole application will be available after you see the passwords. Open the URL ```https://0.0.0.0/``` in a web-browser. You should see the Kasm Workspaces login screen. Login as ```admin@kasm.local```.
5. Enable 2FA
    1. Navigate to `Access Management` -> `Groups`
    2. Click *Edit* on the `All Users` group
    3. Click the `Settings` tab
    4. Click the `Add Settings` Button
    5. Add `enable_totp_two_factor`
    6. Log out and then back in to enable the code generation