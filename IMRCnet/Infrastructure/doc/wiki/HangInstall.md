## CIRC Wiki - Hangtown Windows 11 Development Virtual Machine
[Home](Home)
# Installation

Reference: [SysGuides](https://sysguides.com/install-a-windows-11-virtual-machine-on-kvm)

## Prerequisite

* Windows11 ISO on host's /opt
* `virtio-win.0.127.iso` on /opt

## OS Setup

* In Virtual Machine Manager, press '+' to Create a new virtual machine
  * Select Local install media (ISO)
  * Select Archtecture: x86-64
  * Press [Forward]
  * [Browse] to /opt and select `Win11_24H2_English_x64.iso`
  * Press [Choose Volume]
  * If Microsoft Windows 11 has not been detected, specify
  * Press [Forward]
  * Specify 8192 MB (half) and 3 CPUs (available minus 1)
  * Press [Forward]
  * Specify 256 GB virtual disk image
  * Press [Forward]
  * Specify name: Hangtown and NAT Network
  * Check [Customize]
  * Press [Finish]

* Customize VM Installation
  * Overview Tab, Details
    * Make sure `Q35` and `UEFI` are selected
  * Overview Tab, XML
    * <hyperv/> section
```
<hyperv mode="custom">
  <relaxed state="on"/>
  <vapic state="on"/>
  <spinlocks state="on" retries="8191"/>
  <vpindex state="on"/>
  <runtime state="on"/>
  <synic state="on"/>
  <stimer state="on">
    <direct state="on"/>
  </stimer>
  <reset state="on"/>
  <vendor_id state="on" value="KVM Hv"/>
  <frequencies state="on"/>
  <reenlightenment state="on"/>
  <tlbflush state="on"/>
  <ipi state="on"/>
  <evmcs state="on"/>
</hyperv>
```
    * In <clock/> section, Add if necessary:
    * `<timer name="hypervclock" present="yes"/>`
    * Press [Apply]
  * CPUs Tab, Details
    * Make sure check: host-passthrough
    * Press [Apply] if necessary
  * SATA Disk 1, Details
    * Specify Disk bus: VirtIO
    * In Advanced options, 
    * Specify Cache mode: none
    * Specify Discard mode: unmap
    * Press [Apply] if necessary
  * Press [Add Hardware]
    * Select Storage
    * Select Device type: CDROM on bus: SATA
    * Press [Manage] and set Win11....iso
    * Press [Finish]
  * NIC, Details
    * Specify Device model: virtio
    * Press [Apply]
  * Tablet
    * Press [Remove], if present, and [Yes] to confirm
  * Press [Add Hardware]
    * Channel, Details
    * Select Name: org.qemu.guest_agent.0
    * Press [Finish]
  * TPM
    * In Advanced options, 
    * Select Version: 2.0
    * Press [Apply]
  * Click Begin Installation

* In Hangtown Virtual Machine Installation:
  * Press [Any Key] to begin from virtual CDROM
  * Select English/US, no product key, [Accept/Next/Install], etc. for Win11 Pro installation
  * On Selecting disk destination,
    * Click Load driver
  * Specify Personal, Apply Updates

* Network Setup
  * Install VirtIO Drivers
  * Specify fixed IP Address: 192.168.2.123

## Baseline Software

### Chrome

### 





  