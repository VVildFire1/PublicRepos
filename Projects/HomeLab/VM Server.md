This one is starting out like my Router build but this will be a 1U rack I was going to run windows server as a VM on here so that will go in after proxmox


Major change due to this server having a iDRAC I did my install of the os in this. I will not be going over this in detail but i turned off raid and booted to this and used the lifecycle manager to use a virtual CD drive for the ISO I will leave the Rufus info here for any one who wants to make the drive that way.

## Hardware Components

PowerEdge Dell R630 Server | 2X E5-2695 v4 = 36 Cores | 256GB RAM | 2X 480GB SSD https://amzn.to/48QTGSG

## Software Preparation

Downloading and setting up Proxmox Virtual Environment as the main operating system.

- Download Proxmox VE: [Proxmox Download](https://www.proxmox.com/en/)

### Creating a Bootable Flash Drive

To write the Proxmox image to a USB flash drive, I'm using Rufus:

- Rufus: [Download Rufus](https://rufus.ie/en/)

#### Making the Bootloader

1. Ensure the USB drive is empty or that no required data is on it.
2. Open Rufus, click 'Select' and locate the Proxmox ISO file.
3. Confirm the device is the intended flash drive and press 'Start'.

Note: During this process, it's normal for Windows to report the drive as unreadable.

## Installing Proxmox

### Steps for Installation

1. Boot from the USB, and when prompted by the Proxmox installer, select the GUI install option.
2. Set your timezone, and provide an email and password for server alerts.
3. For the network setup, temporarily use existing network details. Post-setup, IP addresses and FQDNs will be configured.
   - If unsure, you can use a placeholder like `proxmox.home.arpa`.
4. Review the summary, confirm the settings, and proceed with the installation.
5. Post-install, access the Proxmox interface via the web browser at the IP set during installation on port `8006`.

### Troubleshooting

If there's an IP conflict or a need to change network settings:

1. Log in as `root` using the password set during installation.
2. Open the network configuration file:

    ```bash
    nano /etc/network/interfaces
    ```

3. Modify the IP address as needed, save the file, and reboot the system.


<img src="/Projects/images/proxmoxhome.png">

![](proxmoxhome.png)

---
