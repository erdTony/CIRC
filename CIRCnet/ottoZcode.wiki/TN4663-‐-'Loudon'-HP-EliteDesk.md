## TechNote 4663
# 'Hales' HP EliteDesk

## Hardware

* HP EliteDesk 800s Mini
* 16GB RAM (Short DIMM)
* 512GB SSD

## Partitions

* Boot: 500MB FAT32 Windows Boot Manager 
* ? Windows Reserved: 128MB [sda2]
* `LoudonWinSys`: 260GB - NTFS Windows System [C:\ sda3]
* `LoudonHome2`: 32GB - NTFS Shared [S:\ sda4]
* `LoudonNixSys`: 188GB - ext4 Ubuntu Studio root [sda5?]

## BIOS

* Boot Keys
  * Esc - BIOS/UEFI Setup
  * F9 - Boot Device Menu

