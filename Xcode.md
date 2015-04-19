## Xcode CLI Commands

#### List Simulator Devices

`xcrun simctl list`

#### Get UUID of Currently Booted Simulator Device

`xcrun simctl list|grep Booted|awk '{print $3}'|sed -e 's/(//g'|sed -e 's/)//g'`
