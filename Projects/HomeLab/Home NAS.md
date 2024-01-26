
# TrueNAS Server Setup

I'm embarking on an exciting journey to build a TrueNAS server. Here's a breakdown of the hardware I'm using and my planned configuration.

## Hardware Components

### Server Cabinet
- **WEBTB 4U Server Cabinet**: A sturdy and spacious cabinet to house all the hardware.
  - [Amazon Link](https://amzn.to/47K52qk)

### Hard Drives
- **2x MDD 12TB Internal Enterprise Hard Drive**: For substantial storage capacity in a ZFS configuration.
  - [Amazon Link](https://amzn.to/48LDTo1)

### Solid State Drives
- **Patriot P210 1TB Internal SSD**: For efficient and fast data access.
  - [Amazon Link](https://amzn.to/48DPIg9)
- **T-Force Vulcan Z 512GB Internal Solid State Drive SSD**: Additional SSD for enhanced storage performance.
  - [Amazon Link](https://amzn.to/3HylyiA)

### Motherboard, CPU, and RAM
- **Existing Asus Motherboard, CPU, and RAM**: Repurposing an old Asus motherboard with 8 SATA ports, making it an ideal candidate for a NAS system.

## TrueNAS Configuration

### Operating System
- **TrueNAS**: An open-source and robust OS, perfect for network-attached storage solutions.

### Storage Setup
- **ZFS Configuration**: The 12TB drives will be set up in a ZFS pool for redundancy and data integrity.
- **Boot Drive**: One of the SSDs will be utilized as the boot drive for TrueNAS.
- **Cache and Metadata Drive**: The other SSD will be dedicated to caching and metadata for services like Jellyfin, enhancing media streaming performance.

## Goals and Expectations

With this setup, I aim to create a reliable and high-capacity storage solution, suitable for both personal and potentially small business use. The TrueNAS system will allow for efficient data management, media streaming, and secure storage options.

Stay tuned for updates as I progress with the build, including detailed setup steps, configuration challenges, and performance insights.

---

## Software Preparation

Downloading and setting up TrueNAS as the main operating system.

- Download TrueNas: [TrueNas Download](https://www.truenas.com/)

### Creating a Bootable Flash Drive

To write the TrueNas image to a USB flash drive, I'm using Rufus:

- Rufus: [Download Rufus](https://rufus.ie/en/)

#### Making the Bootloader

1. Ensure the USB drive is empty or that no required data is on it.
2. Open Rufus, click 'Select' and locate the TrueNas ISO file.
3. Confirm the device is the intended flash drive and press 'Start'.
4. It may ask you what mode you want DD

Note: During this process, it's normal for Windows to report the drive as unreadable.

## Installing TrueNas

### Steps for Installation

1. Boot from the USB, and when prompted by the TrueNAS to start  the install follow the steps
2. when it ask what drive to install it to I used my 1TB drive for the OS
3. It will ask you to make a Admin password
4. then the OS will start to install it self.
5. when it boots up it will give you what IP it is on. from here you can log on your web browser and goto the the IP or pick a option  I will be going to the IP also I will be giving my server a static IP in my firewall.

---



# Configuring the TrueNAS Server

With TrueNAS installed and the initial login complete, the next steps involve configuring the storage, setting up network shares, and optimizing performance.

## Initial Configuration

### Accessing the TrueNAS Web Interface
1. Open a web browser and enter the IP address of your TrueNAS server.
2. Log in using the credentials you created during the installation process.

### Updating TrueNAS
- It's a good practice to check for any available updates to TrueNAS and apply them to ensure you have the latest features and security patches.

## Storage Configuration

### Setting Up Hard Drives

#### 12TB Hard Drives Configuration
Configuring your 12TB hard drives correctly is crucial for data integrity and performance. Here's how to set them up in a ZFS pool:

1. **Navigate to Storage Settings**:
   - In the TrueNAS web interface, go to `Storage -> Ctrate Pool`.
   - This section is where you can manage all storage-related configurations.

	   

2. **Create a New ZFS Pool**:
      - You will be presented with options for naming your pool and selecting the disks to include.
	      1. Name your pool
	      2. Pick a Layout I will be using Mirror
	      3. I will have a Width of 2 (2 drives) and number of VDEVs as 1
	      4. I will not be useing a ZFS log since my data will be more media not live data, as well as no spare and just clicking next on the rest of the options


3. **Advanced Settings (Optional)**:
   - You can adjust advanced settings like compression, deduplication, and encryption based on your needs.
   - Compression can save space with minimal performance impact.
   - Deduplication, while useful for certain workloads, can be very RAM intensive.
   - Encryption adds security but may impact performance.

4. **Creating the Pool**:
   - After configuring the settings, click `Create` to finalize the pool.
   - The system will prompt you to confirm the creation of the pool, as this process will erase any existing data on the selected drives.

7. **Post-Creation Steps**:
   - Once the pool is created, it will appear in the `Storage.
   - You can now create datasets or zvols on this pool, depending on how you plan to organize and use your storage.

I will now be doing this for the SSD I want to use as a metadata drive for jellyfin

---

## Network Shares and Services Setup

### Creating Network Shares
- Depending on your needs (e.g., Windows or macOS clients, media devices), set up appropriate shares:
  - For Windows clients, configure SMB shares.
  - For macOS, set up AFP or SMB shares.
  - For mixed environments, NFS shares can be a good option.

## Setting Up User Accounts and Datasets in TrueNAS

### Creating a User Account

1. **Accessing User Management**:
   - In the TrueNAS web interface, go to `Credentials -> Local Users`.
   - This section allows you to manage user accounts on your TrueNAS system.

2. **Adding a New User**:
   - Click on `Add` in the top right corner.
   - Fill in the details for the new user:
     - **Username**: Choose a unique username for the account.
     - **Password**: Set a strong password for the account.
   - The other settings can be left at their default values unless specific changes are required.
   - Click `Save` to create the new user account.

### Creating Datasets for Storage

1. **Navigating to Datasets**:
   - On the left-hand menu, select `Datasets`. This option is under the storage section.

2. **Adding a New Dataset**:
   - Click on `Add Dataset` located at the top right, ensuring you are on the correct drive (the one you set up previously).
   - Create a dataset named `Programs`:
     - **Dataset Name**: Enter `Programs`.
     - Configure additional settings as needed.
     - Click `Save` to create the dataset.
   - Repeat the process to create another dataset:
     - This time, name the dataset `Media`.
     - Follow the same steps and click `Save`.

By following these steps, you will have a user account set up for accessing and managing the TrueNAS system, and two datasets named `Programs` and `Media` for organizing your storage. These datasets can be used to store and manage different types of data, such as applications in `Programs` and multimedia files in `Media`.

### Additional Services
- Consider enabling services like Apple Time Machine support, FTP, or WebDAV as per your requirements. It will now ask for user informations I will be useing this as my Jellyfin Server












## Monitoring and Management

### Setting Up Alerts
- Configure email or other alert mechanisms to be notified in case of issues with the server.

### Monitoring System Health
- Regularly check the `Dashboard` and `Reports` sections in the TrueNAS interface to monitor system health, disk usage, and other performance metrics.

## Next Steps

- **Testing**: Ensure all network shares are accessible and perform read/write tests.
- **Backup Plan**: Implement a backup strategy for your data.
- **Documentation**: Keep a record of your configurations and changes for future reference.

## Conclusion

Your TrueNAS server is now set up with a robust storage configuration and initial network services. As you become more familiar with TrueNAS, explore additional features and optimize the system to suit your specific needs.

Stay tuned for further updates and enhancements to this TrueNAS server setup.



