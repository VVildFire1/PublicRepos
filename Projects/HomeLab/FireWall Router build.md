Ok so my Hard ware has arrived


MOGINSOK 4x 2.5GbE Mini PC [[Amazon Link](https://amzn.to/4aKXqXf)] - Features a 12th Gen Intel Core i3 N305 processor (up to 3.4GHz and 8 Cores) I got the barebones

Timetec 32GB DDR5 4800MHz [[Amazon Link](https://amzn.to/48tV9y7)] 

PNY CS1030 1TB M.2 NVMe PCIe Gen3 x4 Internal Solid State Drive (SSD) [[Amazon Link](https://amzn.to/3HeBu9C)]

First thing I need to do is install the Ram and the SSD. This item is a lot smaller then I thought but that's a good thing. Ram fits no problem and there is 2 M.2 ports. Might upgrade and add a 2nd SSD later not sure right now. 

Downloading ProxMox Virtual Environment this is going to be my main boot OS
https://www.proxmox.com/en/

After Downloading this i will need to write the iso to a Flashdrive the image is under 2 GB so thats not to hard.

To do this i will be using Rufus https://rufus.ie/en/ I have been useing this program for awhile for my Pi and other things and it is easy


# Making the Boot loader

Step 1. Make sure the USB I am going to flash in Blank or i dont need the data on it.

Step 2. click select on Rufus and find your ISO. 

Step 3. Make sure the Device is set to your Flash drive and click start.

wow that was so hard. any way now we just wait for the drive to be completed it might say that the drive is unreadable at this time but that's normal for windows

# Installing Proxmox

The next steps will be getting the system up and running. I plan to run this headless (no screen keyboard etc) but for now i connect it to a screen keyboard mouse and cat5 then the USB and press the power button

Step 1. Booting the device moves the the proxmox Installer and asked how to install I pick the first one for GUI install. 

Step 2. Answer the questions for your Timezone  and then it will ask you for a Email and Password. this is where it will send msg if there is a problem with you server if you set that up later.

Step 3. now it will ask for your network info for now I will use just my old info since once this is up and running I will be seeting up new IPs and a FSDN for my self. if you are noot sure what to put in use somthing like proxmox.home.arpa

Step 4. It will give you a summery to make sure everting is good then you can click install with the check mark to reboot after install

Step 5. if evething worked ok you should be able to to open your web browser to the IP that you put in. or it will show up on the command. on port 8006

Troubleshooting 
If you picked an IP that is already used or need to change it follow this

Log in with root and the password you gave it then do the following

```
nano /etc/network/interfaces
```

you will see and address change it to what you need save the file and reboot I had to do this

<img src="/Projects/images/proxmoxhome.png">

![](proxmoxhome.png)
