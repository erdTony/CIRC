## EIRC CIRC Wiki
[Home](Home)
# Hales Network Setup

## Fixed IP Addresses

The preference for each of the entries in the [Host List](Host%20List) 
is for them to set their own fixed IP address. 
The remainder will be set by the fixed DHCP records on the BEC Router.

For Hales-itself (and other Ubuntu-based hosts):

* $ `ip a` _to list the network interfaces_
* $ `cd /etc/netplan` _look for a network configuration file_
* $ `sudo cp 01-network-manager-all.yaml 01-network-manager-all.yaml.000` _back it up_
* $ `sudo nano 01-network-manager-all.yaml`
* Enter the text below: **Indentation is important**
```
    network:
      version: 2
      renderer: networkd
      ethernets:
        eno1: # Network Identified Above
          dhcp4: no
          addresses: [192.168.2.12/24] # Your static IP and netmask
          gateway4: 192.168.2.1 # Your router's IP
          nameservers:
            addresses: [192.168.2.1, 8.8.8.8, 8.8.4.4] # DNS server IPs
```
* $ `sudo netplan apply`
* $ 'ip a' # to test

_NOTE: Gateway4 is depricated. Address as a Default Route instead_

## OpenSSH Server

Reference: [nixCraft](https://www.cyberciti.biz/faq/ubuntu-linux-install-openssh-server/)

* $ `sudo apt-get install openssh-server`
* $ `sudo systemctl enable ssh`
* $ `sudo systemctl start ssh`
* $ `sudo systemctl status ssh` _To Test_

Pass SSH (Port 22) through firewall:

* $ `sudo ufw allow ssh`
* $ `sudo ufw enable`
* $ `sudo ufw status` _To Test_

Try on another *nix/*BSD system:

* $ `ssh ftp@192.168.2.12`
* Password: ftp
* $ `exit` _When finished_

## Attach 1TB Share

* $ `lsblk` _List Block Devices to find USB drive_
* Identified `sdb` USB device with shared partition `sdb2`
* $ `sudo mkdir /mnt/usb_sdb2`
* $ `sudo mount /dev/sdb2 /mnt/USB1TShareA`

## SMBD & NFS Sharing

* $ `sudo apt install samba acl`
* $ `cd /etc/samba`
* $ `sudo cp smb.conf smb.conf.001`
* $ `sudo nano smb.conf`
* Change: `workgroup = CIRCnet`
* Add:
```
[local1A]
  comment = Samba on Hales Ubuntu Host
  path = /mnt/USB1TShareA
  readonly = no
  browsable = yes
```
* Save smb.conf

### SMB Users

* ...TBD

## GitKraken Desktop

Reference:  https://snapcraft.io/gitkraken

* $ `sudo snap install gitkraken --classic`

 
## RustDesk Client

* Download `rustdesk-v#.#.#-x86_64.deb` from [github](`https://github.com/rustdesk/rustdesk/releases`)
* $ `sudo apt install ./rustdesk-<version>.deb`
* Run RustDesk
  * Click &#8942;, Select Security tab, and press Unlock Security
  * Select Permanent Password and enter password & confirmation: CIRChales7
  * Back to Home, Note ID `530 850 204`


