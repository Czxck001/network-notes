# Setting up Ubuntu Server 18.04 LTS

## Connect to the Internet

### Get your netcard name

`ip addr`

### Configurate DHCP or static IP

See [this article](https://websiteforstudents.com/configure-static-ip-addresses-on-ubuntu-18-04-beta/).

> Have you heard of NetPlan? Probably not, if you have, then you’re a step ahead of many. NetPlan is a new network configuration tool introduced in Ubuntu 17.10 to manage network settings.
>
> This new tool replaces the static interfaces (**/etc/network/interfaces**) file that had previously been used to configure Ubuntu network interfaces. Now you must use **/etc/netplan/\*.yaml** to configure Ubuntu interfaces.
>
> Run the commands below to create a new network configuration file
>
> `sudo nano /etc/netplan/01-netcfg.yaml`
>
> Below is a sample file for a network interface using networkd as renderer using DHCP. Networkd uses the command line to configure the network interfaces.`
>
> ```yaml
> network:
>  version: 2
>  renderer: networkd
>  ethernets:
>    ens33:  # change this key to your netcard name
>      dhcp4: yes
>      dhcp6: yes
> ```
>
> Exit and save your changes by running the commands below:
>
> `sudo netplan apply`
>
> ...
>
> Then configure IPv4 addresses as shown below… take notes of the format the lines are written…
>
>  ```yaml
> # This file describes the network interfaces available on your system
> # For more information, see netplan(5).
> network:
>  version: 2
>  renderer: networkd
>  ethernets:
>    ens33:
>      dhcp4: no
>      dhcp6: no
>      addresses: [192.168.1.2/24]
>      gateway4: 192.168.1.1
>      nameservers:
>        addresses: [8.8.8.8,8.8.4.4]
>  ```
>
> You can add IPv6 addresses line, separated by a comma.. example below.
>
> ```yaml
> # This file describes the network interfaces available on your system
> # For more information, see netplan(5).
> network:
>  version: 2
>  renderer: networkd
>  ethernets:
>    ens33:
>      dhcp4: no
>      dhcp6: no
>      addresses: [192.168.1.2/24, '2001:1::2/64']
>      gateway4: 192.168.1.1
>      nameservers:
>        addresses: [8.8.8.8,8.8.4.4]
> ```

## Install drivers (e.g. Nvidia graphics card)
See [this article](https://linuxconfig.org/how-to-install-the-nvidia-drivers-on-ubuntu-18-04-bionic-beaver-linux).

```
sudo ubuntu-drivers autoinstall
```

## Install CUDA
See [this article](https://askubuntu.com/questions/1028830/how-do-i-install-cuda-on-ubuntu-18-04).

```
sudo apt install nvidia-cuda-toolkit gcc-6
nvcc --version
```
