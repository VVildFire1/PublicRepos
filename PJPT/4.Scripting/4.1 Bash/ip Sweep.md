# IP Sweep Script

A bash script to perform an IP sweep (ping scan) on a local network to identify which IP addresses are active.

## Script Content

```bash
#!/bin/bash
# Check if an IP address is provided as an argument
if [ "$1" == "" ]
then
    echo "You forgot an IP address!"
    echo "Syntax: ./ipsweep.sh 192.168.1"
else
    # Loop through the possible host addresses (1 to 254)
    for ip in `seq 1 254`; do
        # Ping each address with a single echo request
        ping -c 1 $1.$ip | grep "64 bytes" | cut -d " " -f 4 | tr -d ":" &
    done
fi
```

## Usage

The script takes the first three octets of an IP address as an argument and pings the range of possible addresses from 1 to 254. If a device is up and responds to the ping, its IP address is printed to the terminal.

## Example

To use the script, save it as `ipsweep.sh`, give it execution permissions with `chmod +x ipsweep.sh`, and run it with a network address prefix like so:
```bash
./ipsweep.sh 192.168.1
```

## Note

The script runs ping commands in the background in parallel due to the `&` at the end of the ping command. This speeds up the sweeping process. It filters the ping response to display only the IP addresses that responded with "
