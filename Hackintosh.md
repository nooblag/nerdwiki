# Hackintosh

__DISCLAIMER__: please don't steal, [buy stuff from Apple](https://apple.com)!

## ASUS P8-H67-M Pro

### 10.7

#### MultiBeast post-install

- Use `DSDT Auto-Patcher` and save `DSDT.aml` to desktop. select user DSDT in MultiBeast(?)
- Delete kext `appletymce.kext` to prevent kernel panic
- Graphics: `PCIRootUID=0` for Nvidia 240GT graphics to enable

### 10.9

- [Make bootable USB using this method](http://www.tonymacx86.com/374-unibeast-install-os-x-mavericks-any-supported-intel-based-pc.html)
- To install to an MBR partition, [get files from here](http://www.insanelymac.com/forum/files/download/145-mavericks-mbr-patch/), and [update the USB stick using this method](http://www.macbreaker.com/2012/08/mountain-lion-mbr-unibeast.html)
- If stuck on grey screen once installed and on welcome screen; unplug display from graphics card before getting to grey screen

#### MultiBeast post-install

- Install `NullCPUPowerManagement`

### 10.10

- [Make bootable USB using this method](http://www.tonymacx86.com/445-unibeast-install-os-x-yosemite-any-supported-intel-based-pc.html)

#### MultiBeast post-install

- Install `NullCPUPowerManagement`, `TRIM Enabler` (if SSD)
- Ethernet: install `RealtekRTL81xx`
- Audio: install `Realtek ALC892`, Optional HDA Enabler > `Audio ID: 1`

### 10.11

- [Make bootable USB using this method](http://www.tonymacx86.com/threads/unibeast-install-os-x-el-capitan-on-any-supported-intel-based-pc.172672)

#### MultiBeast post-install

Based on version `8.2.3 (1)`

- `Quick Start > Legacy Boot Mode` if fresh install
- `Customize > System Definitions > Mac Pro > Mac Pro 6,1`
- Ethernet: `Drivers > Network > RealtekRTL8111 v2.2.1`
- Audio: `Drivers > Audio > Realtek ALCxxx > ALC892`

## Errors & Workarounds

### App Store login error

- Ensure Ethernet kext is installed and Ethernet is network interface en0
- If not en0, then delete `/Library/Preferences/SystemConfiguration/NetworkInterfaces.plist` and restart
