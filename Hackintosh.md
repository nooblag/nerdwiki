# Hackintosh

## ASUS P8-H67-M Pro

### 10.7

- Combo update to 10.7.5

- MultiBeast after install, use DSDT auto-patcher and save DSDT.aml to desktop. select user DSDT in mutlibeast

- PCIRootUID=0 for Nvidia 240 GT graphics to enable

- delete kext `appletymce.kext` to prevent kernel panic

### 10.9

- Make bootable USB using this method - `http://www.tonymacx86.com/374-unibeast-install-os-x-mavericks-any-supported-intel-based-pc.html`

- To install to an MBR partition, get files from here - `http://www.insanelymac.com/forum/files/download/145-mavericks-mbr-patch/`, and update the USB stick using this method - `http://www.macbreaker.com/2012/08/mountain-lion-mbr-unibeast.html`

- If stuck on grey screen once installed and on welcome screen; unplug display from graphics card before getting to grey screen

- MultiBeast post-install - install NullCPUPowerManagement

### 10.10

- Make bootable USB using this method - `http://www.tonymacx86.com/445-unibeast-install-os-x-yosemite-any-supported-intel-based-pc.html`
