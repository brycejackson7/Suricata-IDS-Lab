# Suricata-IDS-Lab

This project documents the installation and configuration of **Suricata**, an open-source intrusion detection system (IDS), and testing it with simulated malicious traffic.

---

## Environment Setup

I built a lab environment with one VM in VirtualBox:

- **Ubuntu Server** – running Suricata IDS

### Network Configuration
The VM was configured on a NAT network with IPv4 prefix 192.168.10.0/24 and DHCP enabled.

## Suricata Installation & Configuration

On the Ubuntu Server:

1. Installed Suricata using the package manager:

    ```bash
    sudo apt update
    sudo apt install suricata -y
    ```

2. Updated the network interface in `/etc/suricata/suricata.yaml`:

    ```yaml
    interface: enp0s3
    ```

3. Configured the home network variable (`HOME_NET`) to match the lab network:

    ```yaml
    vars:
      address-groups:
        HOME_NET: "[192.168.10.0/24]"
    ```

4. Tested the Suricata configuration:

    ```bash
    sudo suricata -T -c /etc/suricata/suricata.yaml -v
    ```

    ![Suricata config success](images/suricata%20config%20success.png)

    Successful output confirmed the configuration loaded without errors.

## Generating Test Alerts

To verify IDS functionality:

1. Used curl to access [httptestmynids.org](http://httptestmynids.org) and generate simulated malicious traffic.  
2. Checked Suricata logs:

    ```bash
    cat /var/log/suricata/fast.log
    ```

![Suricata Test](images/suricata%20test.png)

Suricata successfully detected the simulated malicious activity and generated alerts in `fast.log`.

## Summary

- Updated the Suricata network interface and home network.  
- Verified configuration successfully.  
- Generated and confirmed test alerts using simulated malicious traffic.  

This lab demonstrates the basic deployment of Suricata as a network IDS in a virtualized lab environment.
