# Homelab Setup Guide

Welcome to my step-by-step guide for setting up my Homelab with Proxmox VE and high-performance hardware.

## Hardware Arrival

My new hardware has arrived and it's time to get everything set up:

- **MOGINSOK 4x 2.5GbE Mini PC**:
  - 12th Gen Intel Core i3 N305 processor (up to 3.4GHz and 8 Cores). Opted for the barebones version.
  - [Amazon Link](https://amzn.to/4aKXqXf)

- **Timetec 32GB DDR5 4800MHz RAM**:
  - [Amazon Link](https://amzn.to/48tV9y7)

- **PNY CS1030 1TB M.2 NVMe PCIe Gen3 x4 SSD**:
  - [Amazon Link](https://amzn.to/3HeBu9C)

### Initial Setup

The first step involves installing the RAM, which fits seamlessly into the slots, and the SSD into one of the two available M.2 ports. The compact size of the Mini PC is a plus for space management. Considering a future upgrade with an additional SSD.

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


# Setting Up PFsense as the First VM on Proxmox

Having a functional VM server, it's time to set up PFsense as our first Virtual Machine.

## Uploading PFsense ISO to Proxmox

There are two ways to get the PFsense ISO into Proxmox:

1. **Downloading Directly via URL**:
   - You can use Proxmox's feature to download the ISO directly from a URL.

<img src="/Projects/images/isoupload.png">
![](isoupload.png)

2. **Uploading a Downloaded ISO**:
   - Alternatively, if you have already downloaded the ISO, you can upload it to Proxmox.
   - Ensure to unzip the ISO file before uploading.
   - Download PFsense from [pfsense.org](https://www.pfsense.org/).


## Creating the PFsense VM

To create the PFsense VM, follow these steps:

1. **Initiate VM Creation**:
   - Click on `Create VM` in the top right corner of the Proxmox interface.


<img src="/Projects/images/cvm.png">
![](cvm.png)
- Name your VM and decide whether it should start at boot. I'll configure the auto-start later after making some adjustments.

2. **Selecting the ISO Image**:
   - Choose the PFsense ISO image you uploaded.



<img src="/Projects/images/vmos.png">
![](vmos.png)

3. **Configuring VM Resources**:
   - Under 'Disk', allocate 25GB of storage (though 16GB should be sufficient).
   - Based on PFsense's [hardware requirements](https://www.pfsense.org/products/), the minimum is 1 GHz CPU and 1 GB RAM. However, I'm assigning 2 CPU cores and 4GB RAM considering the capacity of my system.

4. **Network Configuration**:
   - Choose 'No network device' for now, as we will configure the network interfaces later, especially for WAN and LAN setups.



<img src="/Projects/images/vmnw.png">
![](vmnw.png)

5. **Finalize and Create VM**:
   - Complete the setup and click `Finish`. Proxmox will prepare the VM for the first boot.

After the VM is set up, the next steps will involve booting PFsense for the first time, going through its installation process, and configuring network interfaces and firewall settings.


---

## Network Configuration for PFsense VM in Proxmox

After initially setting up the PFsense VM without a network, it's now time to configure the network interfaces.

### NIC Passthrough

We aim to pass through the Network Interface Card (NIC) directly to the VM. This setup gives PFsense direct control over the NICs, reduces latency, and ensures that these NICs are exclusively used by PFsense.

#### Why NIC Passthrough?

- **Lower Latency**: Direct control over the hardware results in better performance.
- **Exclusive Access**: Ensures that no other VMs share these NICs, which is critical for a router/firewall setup.

#### Steps to Configure NIC Passthrough

1. **Access the Shell in Proxmox**:
   - Open a shell session in Proxmox by clicking on the `Shell` option under your main node.

2. **Edit the GRUB Configuration**:
   - We need to modify the GRUB bootloader configuration to enable IOMMU, which is necessary for passthrough.
   - Use the `nano` editor to open the GRUB configuration file:

     ```shell
     nano /etc/default/grub
     ```


<img src="/Projects/images/nanogrub.png">
![](nanogrub.png)

   - Add the following parameters to the GRUB_CMDLINE_LINUX_DEFAULT line:
     ```
     intel_iommu=on
     ```
     Replace `intel_iommu=on` with `amd_iommu=on` if you're using an AMD processor.

3. **Update GRUB and Reboot**:
   - After saving the changes, update GRUB and reboot your Proxmox server:

     ```shell
     update-grub
     reboot
     ```


## Additional Note on IOMMU Settings for PCIe Passthrough

### Improving PCIe Passthrough Performance

When configuring NIC passthrough in Proxmox for the PFsense VM, adding `iommu=pt` to the GRUB configuration line can enhance the performance of PCIe ports. This setting optimizes the Input/Output Memory Management Unit (IOMMU) for passthrough devices.


```shell

GRUB_CMDLINE_LINUX_DEFAULT="quiet intel_iommu=on iommu=pt"
```
     
   - For AMD processors, it would be:

```shell
GRUB_CMDLINE_LINUX_DEFAULT="quiet amd_iommu=on iommu=pt"
```

### Why `iommu=pt`?

- **Improved Performance**: The `iommu=pt` (passthrough) option can reduce overhead and improve the efficiency of PCIe passthrough devices.
- **Stability**: It can also contribute to the stability of the VMs using the passthrough devices, especially under heavy I/O loads.

By adding this option, you're ensuring that your setup is not only functionally correct but also optimized for the best possible performance with your hardware.

after doing this I like to open the file again just to make sure my changes saved


### Finalizing IOMMU Settings for NIC Passthrough

With the GRUB configuration updated, the next step involves ensuring the necessary VFIO modules are loaded for successful NIC passthrough.

#### Loading VFIO Modules

1. **Add VFIO Modules**:
   - After modifying the GRUB configuration, you need to specify the VFIO modules to be loaded at boot. This is done by editing another configuration file.
   - Open the modules file:

     ```shell
     nano /etc/modules
     ```


<img src="/Projects/images/mods.png">
![](mods.png)

   - Add the following lines at the end of the file:

     ```shell
     vfio
     vfio_iommu_type1
     vfio_pci
     vfio_virqfd
     ```

   - These modules are responsible for facilitating the passthrough of PCIe devices like NICs to your VMs.

2. **Verify and Reboot**:
   - After saving the file, it's a good practice to reopen it to confirm that your changes were correctly saved.
   - Once verified, reboot your Proxmox system to apply these changes:

     ```shell
     reboot
     ```

### Considerations and Troubleshooting

- This process can be complex and may vary based on your specific hardware and Proxmox version.
- If you encounter issues, verify that IOMMU is enabled in your BIOS/UEFI settings.
- Remember, once a NIC is passed through to a VM, it cannot be used by the Proxmox host or other VMs.

By completing these steps, your PFsense VM will have direct control over the specified network interfaces, optimizing its performance as a router/firewall.


---


## Verifying IOMMU Settings and NIC Passthrough Configuration

After rebooting, it's essential to ensure that the IOMMU settings are correctly enabled and functioning.

### Confirming IOMMU Activation

1. **Check for IOMMU Error Messages**:
   - Upon rebooting, look out for any error messages related to IOMMU, such as 'no iommu detected.'
   - If you still see an error message, revisit the previous steps to ensure all edits to the GRUB configuration and module settings are correct.

### Setting Up NIC Passthrough in Proxmox

Now that IOMMU is verified, it's time to pass the network interfaces through to the PFsense VM.

1. **Selecting NICs for Passthrough**:
   - Navigate to the Proxmox web interface and go to your PFsense VM's hardware configuration.
   - Click on `Add` and choose `PCI Device`.
   - Select `Raw device` and `All Functions`, then choose the NICs for passthrough.

<img src="/Projects/images/addpci.png">
![](addpci.png)


2. **Avoiding Proxmox's Active NIC**:
   - Be cautious not to include the NIC currently used by Proxmox itself.
   - In my case, since Proxmox is using port 0, I will pass through NICs on ports 1, 2, and 3.

3. **Applying Changes to VM**:
   - After selecting the NICs, save your changes and start your PFsense VM.

### Post-Configuration Steps

- **Boot PFsense VM**:
  - Once you start the VM, PFsense should recognize the passed-through NICs and utilize them for its network configurations.
  
- **Troubleshooting**:
  - If your Proxmox host loses network connectivity or if the PFsense VM doesn't recognize the NICs, double-check the port numbers and ensure the correct NICs are being passed through.

By following these steps, you've successfully allocated dedicated NICs to your PFsense VM, optimizing your Homelab's network setup. This configuration allows PFsense to manage these interfaces directly, enhancing performance and security.

Congratulations, you've successfully configured NIC passthrough for your PFsense VM! This setup will ensure dedicated and optimized network performance for your Homelab's router/firewall.

---

# Booting up pfSense and Initial Setup

With the VM and network interfaces properly configured, it's time to boot up pfSense and begin the initial setup process.

## Starting pfSense Installation

When you start your VM, it should boot into the pfSense setup:


<img src="/Projects/images/pfsinstall.png">
![](pfsinstall.png)

Follow the on-screen instructions, which will mostly involve clicking 'Next'. 

## Choosing File System

- I opted for the Auto ZFS Guided setup. You might see a warning about having less than 8GB of RAM, but for our purposes, this isn't a concern as we're not using it as a full-fledged NAS.

## Disk Configuration

- During the ZFS configuration, select your drive for installation. In my case, there's only one, so I select it.
- Confirm to overwrite (destroy) the existing data on the drive, as it's just the VM drive.
- After completing the drive setup, the system will ask to reboot.

## Network Configuration

- Upon reboot, you'll be prompted to set up VLANs. I chose 'No' for now, as this can be done later through the GUI.
- Next, it asks for a WAN interface. You can let pfSense auto-detect or choose one. This can be changed later if necessary.
- pfSense will then display the address of your router.

## IP Configuration

- You might face a decision here: create a new network or disconnect and proceed with the existing setup. 
- I'm assigning a new IP to my LAN interface using option 2 since my system isn’t connected to WAN yet.
- Set your router to a static IP and define your subnet (CIDR). For most home networks, `/24` is standard.
- Skip the gateway setting for now, as the pfSense will act as the gateway.
- I chose to disable IPv6 at this point and set up the DHCP range for the LAN.

## Finalizing the Setup

- Opt to keep HTTPS for the web configuration.
- Upon connecting, I receive an IP address and can access the pfSense web interface using the set IP.
- Now, I disconnect the network cable from my old router and connect it to the new pfSense system. 

**Note on Network Transition to pfSense**:
At this stage, I took a significant step in transitioning my network connection from the old router to the new pfSense setup. After plugging the network cable into the pfSense device, it promptly assigned an IP address to my system, allowing me to access the pfSense web interface via the new IP configuration. This successful connection was a gratifying moment, marking a smooth start with the new setup.

### Additional Network Setup Considerations

- **WAN Connection**: If you're ready, you can now disconnect your old router and connect your WAN directly to the new pfSense device. In my case, I held off on this step temporarily because the existing internet connection was still in use by others in my home.

- **Converting Old Router to WiFi Access Point**: My next move involves bridging the old router to serve as a WiFi access point. This transition will ensure continuous wireless network availability throughout this changeover.

- **Dual NIC Configuration on Main PC**: Since my main PC is equipped with two network interfaces (NICs), I connected one to the pfSense system and left the other connected to my existing router. This setup allows me continuous web access during the transition phase and helps in parallel testing and configuration of the new network setup.

you Defalt info

	Username: admin
	Password: pfsense


## Default Login Credentials

- Username: `admin`
- Password: `pfsense`

## Additional Security Measures

For extra security, consider changing the default admin password immediately. You can also create a new user, add them to the admin group, log out, log in as the new user, and disable the default 'admin' account. This adds an extra layer of security, making it more challenging for unauthorized access.


---

# pfSense GUI Setup

After the initial installation and network configuration of pfSense, the next phase involves setting up and customizing the pfSense GUI (Graphical User Interface).

## Quick Start Guide

Upon your first login to the pfSense web interface, you'll typically be greeted with a Quick Start guide. This guide is designed to help you through the basic configuration steps necessary to get your router up and running. 

### Bypassing Quick Start with Hardened Setup

In my case, since I had already performed some advanced configurations and hardening during the installation process, I bypassed the Quick Start guide. This allowed me immediate full control over the router's settings. 

Here's what you need to know about proceeding directly to the main interface:

- **Direct Access to Settings**: Bypassing the Quick Start takes you straight to the main dashboard of pfSense, where you can access all settings and features.
- **Custom Configuration**: You have the flexibility to customize and configure all aspects of pfSense according to your specific needs, without the guided steps.
- **Advanced Features**: For users who are familiar with pfSense or have specific requirements, skipping the Quick Start allows immediate access to advanced features.

## Next Steps

Now that you have access to the full pfSense interface, you can start configuring various aspects of your network:

- **Firewall Rules**: Set up rules to manage incoming and outgoing network traffic.
- **VPN Setup**: Configure VPN services for secure remote access.
- **Network Services**: Adjust settings for DHCP, DNS, and other network services.
- **Monitoring and Maintenance**: Utilize the monitoring tools and schedule regular maintenance tasks.

As you familiarize yourself with the pfSense interface, you'll find a wide range of tools and options to optimize your network's performance and security.


