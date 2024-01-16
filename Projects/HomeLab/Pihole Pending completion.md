# Setting Up Pi-hole as a Virtual Machine on Proxmox 8.1.3

## Preparing Pi-hole Installation

Pi-hole is effectively installed in a containerized environment. With Proxmox 8.1.3, we'll be using a Linux Container (LXC), a lightweight alternative to full machine virtualization, for the Pi-hole setup.

### Creating a Proxmox LXC for Pi-hole

1. **Choose a Linux Distribution for LXC**:
   - Pi-hole works with various Linux distributions. Popular choices for LXC include Ubuntu and Debian. Select a distro that fits your preferences and requirements.

2. **Downloading the Appropriate Template**:
   - Before creating the container, you need to download a template for your chosen Linux distribution.
   - In the Proxmox web interface, navigate to `Datacenter -> Storage -> your_storage -> Templates`.
   - Click the `Templates` button and select your desired Linux distribution from the list to download it. (I will be using Ubuntu 23.10)

<img src="/Projects/images/lxctemp.png">
![](lxctemp.png)

3. **Navigate to LXC Creation in Proxmox**:
   - Go to the 'Create CT' button in the Proxmox interface to start the process of creating a new container.

4. **Container Settings**:
   - Follow the Proxmox wizard to configure your LXC. Key configuration steps include:
     - **Template**: Choose the downloaded template for your chosen Linux distribution.
     - **Storage**: Specify where the LXC disk image will be stored. (I will be giving mine 8Gb)
     - **CPU and Memory**: Allocate adequate resources. Pi-hole is light on resources, but consider your system's overall capacity.(I will be giving mine 1 core since it is not needed much and 2Gb of ram this is way more then needed)
     - **Network**: Set up the network to ensure your Pi-hole container is reachable within your network. (I am letting mine get a DHCP address because i will be setting it as static in my pfSense controls. I also turn the firewall off on the LXC)

5. **Finalizing LXC Creation**:
   - After adjusting all settings, complete the process to create the container.

Once the LXC is set up, you can proceed with the installation of Pi-hole within the container, configuring it to effectively manage DNS and ads on your network.


---
