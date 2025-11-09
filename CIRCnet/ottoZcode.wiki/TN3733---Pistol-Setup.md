## ozCode TechNote 3733
# Pistol Setup

## Hardware
* Lenovo V15 G4 IRU
  * Product # 83A100EGUS
  * Model #83A1
  * Support: V15 G4 IRU Type:83A1
  * Serial #PF4MJQBD
  * BIOS Version: MCCN24WW 9/4/23, UEFI mode
  * SKU: LENOVO_MT_83A1_BU_idea_FM_V15 G4 IRU


* Processor: Intel Core i3-1315u
  * 1.200 GHz
  * 6 cores
  * 8 logical processors
* Memory
  * Physical: 24GB DDR4
  * Virtual: 28GB
  * Page File: 4GB C:\pagefike.sys
* Storage
  * 465GB SSD _???_
    * Kensington #SNV251000G

## OS
* Microsoft Windows 11 Pro
  * v10.0 Build 22621


## Bloatware

**_Replace Factory Win11 Partition_**


## Initial Setup

### Disk Partitions
1. GPT Reserved 
2. GPT Reserved SYSTEM_DRV 260MB
3. [ ] PistolWinSys 384GB NTFS C:\
4. [ ] PistolHome 48GB NTFS shared S:\ /home/shared
5. [ ] /boot/efi for grub eventually
5. [ ] PistolUStud 183GB ext4 root eventually
6. GPT Reserved WINRE_DRV 2GB NTFS

### Baseline Windows Software
- [ ] Chrome web browser
- [ ] TBD
- [ ] S:\Shared from Home2 thumb drive

