
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

