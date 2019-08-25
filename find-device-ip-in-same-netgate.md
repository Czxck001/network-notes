# Find IP of a Device in the Same Netgate

## Step 1: Find `inet` of ethernet interface
```sh
ifconfig
```
Then record the `inet` property of `en0` (the first ethernet interface) or `wlan0` (the first WiFi interface). 
This naming convention is of BSDUnix and might not be the same in Linux.


## Step 2: Scan ports through the interface

In step 1, choose the `inet` of interface that hosts both local PC and the target device. Then, use `nmap` to scan the ports:
```sh
nmap -n -sP INET_IP/24
```
This will list IPs of all devices that are in the same interface. 

The next step would be to take more filtering for these IPs. 

An example is scanning port 22 of SSH by `nmap -p22`:
```sh
nmap -n -sP 192.168.1.30/24 |
grep -E 'Nmap scan report for ([0-9\.]*)' |
awk '{print $NF}' |
xargs nmap -p22 -oG |
grep -B4 open
```
