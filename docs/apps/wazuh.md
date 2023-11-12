![image](../static/images/wazuh/wazuh-headergraphic.png)

## Getting started with Wazuh
Wazuh is a free and open source security platform that unifies XDR and SIEM capabilities. It protects workloads across on-premises, virtualized, containerized, and cloud-based environments.

Wazuh helps organizations and individuals to protect their data assets against security threats. It is widely used by thousands of organizations worldwide, from small businesses to large enterprises.

## Installation

### Container Setup

1. Create a new Ubuntu LXC
    - Name: wazuh
    - CPU: 4 cores
    - Storage: 55 GB
    - Memory: 8200 MB
    - Swap: 4100 MB
    - Network: `static`
2. Update the container  
    ```bash
    apt update && apt upgrade -y; apt autoclean -y; apt autoremove-y
    ```
3. Install Dependencies
    ```bash
    apt install -y curl gnupg apt-transport-https
    ```
4. Install the GPG key
    ```bash
    curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | gpg --no-default-keyring --keyring gnupg-ring:/usr/share/keyrings/wazuh.gpg --import && chmod 644 /usr/share/keyrings/wazuh.gpg
    ```
5. Download and run the Wazuh installation script
    ```bash
    curl -sO https://packages.wazuh.com/4.6/wazuh-install.sh && bash ./wazuh-install.sh -a
    ```

??? note "Password Missed?"
    If the interface lost connection and you didn't see the password, you can run:  

    ```bash  
    tar -O -xvf wazuh-install-files.tar wazuh-install-files/wazuh-passwords.txt
    ```

## Firewall Configuration

From [Wazuh Docs](https://documentation.wazuh.com/current/getting-started/architecture.html) we must port forward or open the following ports:

- 1514 (TCP) for agent connection
- 1515 (TCP) for agent enrollment service