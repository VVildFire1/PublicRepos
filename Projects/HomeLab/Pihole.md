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

On a side note I do a apt update and upgrade to make sure I am up-to-date


---
## Installing Pi-hole

Once your Linux VM is up and running, you can install Pi-hole:

1. **Access the VM Console**:
   - Use the console feature in Proxmox to access your Linux VM.

2. **Install Curl**:
	- Curl will be needed to install pihole
```shell
apt install curl
```

3. **Install Pi-Hole**:
   - Run the Pi-hole installation script in your VM's terminal. You can find the script on the [Pi-hole website](https://pi-hole.net/).
   
```shell
curl -sSL https://install.pi-hole.net | bash
```


4. **Follow the Installation Wizard**:
   - The Pi-hole installer will guide you through the setup, including configuring network settings and selecting DNS options. I like Cloudflare

5. **Completing the Installation**:
   - Once installed, you can access the Pi-hole admin interface via the web browser using your VM's IP address. Make note of the password it gives you

******Extra notes*******
Pihole is not the best when it comes to telling you how to change your password but if you goto a command line in your shell 

```shell
pihole -a -p
```

and this will let you change your password.


Pi-hole is now set up and ready to block ads and manage DNS queries in your network. Enjoy the benefits of a cleaner, faster web browsing experience in your Homelab environment! You can add this on each system you want it on. Or you can add it to our Router so it will give it to evething.

---

1. **Access pfSense Web Interface**:
    	- Log in to the web interface of your pfSense router. 
     
2. **Navigate to DNS Settings**:
    
    - Once logged in, look for the DNS settings. This is usually found under `System` > `General Setup` or `Services` > `DNS Forwarder` or `DNS Resolver`, depending on your pfSense configuration.
3. **Configure DNS Servers**:
    
    - In the DNS settings:
        - Add the IP address of your Pi-hole device as the primary DNS server.
        - You can add secondary DNS servers, but be aware that this can allow traffic to bypass Pi-hole. Some people use another Pi-hole instance or a public DNS service as a backup.
4. **Disable DNS Forwarder/Resolver (Optional)**:
    
    - If you're using Pi-hole for all DNS queries, you might want to disable pfSense's built-in DNS Forwarder or DNS Resolver to prevent DNS leaks. This step is optional and depends on your specific network setup.
5. **Save and Apply Changes**:
    
    - After making these changes, save them and apply the configuration.
6. **Test the Configuration**:
    
    - To test, you can visit a website known to have ads and see if Pi-hole is blocking them. Also, check the Pi-hole dashboard to see if it's receiving queries.
7. **Configure DHCP Server (Optional)**:
    
    - If you use pfSense as your DHCP server, you might want to configure it to advertise the Pi-hole server as the DNS server to clients. Go to `Services` > `DHCP Server` and set the Pi-hole IP as the DNS server for each of your network segments.
8. **Restart Devices**:
    
    - It may be necessary to restart your network devices or renew their DHCP leases to ensure they start using Pi-hole for DNS queries.

Remember, while configuring Pi-hole with pfSense, it's important to consider the implications of DNS settings on your network's performance and security. Always have a backup plan in case you need to revert changes, and document any configurations you modify for future reference


