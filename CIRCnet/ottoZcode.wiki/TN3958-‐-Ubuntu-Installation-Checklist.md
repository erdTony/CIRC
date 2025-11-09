# TN3958 - Ubuntu Installation Checklist
&#x2B09;**[Home](Home)** &#x2B25; &#x2B60;_Back_ &#x2B25; &#x2B61;_Up:_ **[Tech Note Index](Tech-Note-Index)** &#x2B25; &#x2B62;_Next_ &#x2B25; &#x2B69;_First:_ 

<sup>Revised: 2023-10-15</sup>

## Preparation

* [ ] Download Installation ISO disk image for the Unix to be installed. Currently Lubuntu 22.04.3 LTS and Ubuntu Studio 23.10 are installed or planned.
  * [Lubuntu ISO Download](https://cdimage.ubuntu.com/lubuntu/releases/22.04.3/release/lubuntu-22.04.3-desktop-amd64.iso)
  * [Ubuntu Studio ISO Download](https://cdimage.ubuntu.com/ubuntustudio/releases/23.10/release/ubuntustudio-23.10-dvd-amd64.iso)
* [ ] Burn ISO to bootable USB thumb drive
* [ ] Insure unused partition is available on the host hard disk

## Installation

* Boot from ISO thumb drive
  * [ ] Select keyboard, timezone, etc.
  * [ ] Install to desired partitions
    * `/boot/efi` fat32 100MB
    * `/` ext4 root {desired size}
  * [ ] Add primary administrator account `toor:toor`

## Initial Setup

* Boot from primary disk 
  * Update
    * [ ] $ `sudo apt update`
    * [ ] $ `sudo apt upgrade`
  * Create User Accounts [wiki](User-Accounts)
  * Install lxqt desktop
    * Reference: [LinuxHow](https://linux.how2shout.com/install-lxqt-desktop-environment-on-ubuntu-22-04-20-04-linux/)
    * [ ] $ `sudo apt install task-lxqt-desktop`
    * [ ] $ `sudo apt install lxqt`
    * [ ] $ `sudo reboot`