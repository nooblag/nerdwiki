## Linux from scratch

### Errors and workarounds

Using mkswap, get error 'need 40kb space or more'

Make sure swap partition is not an extended partition; reboot so it can read partition table again.


Error at chapter 5.9 binutils 2nd pass
kernel too old

kernel version 2.6.22.5 glibc compiled in chapter 7
2.6.16.38 host is older kernel

solution is update the kernel; make sure livecd has correct kernel


after pause and resume, get error 'c compiler cannot create executables' when trying to compile.

solution is make sure this line is in .bashrc - LFS_TGT=$(uname -m)-lfs-linux-gnu

resume document on website does not include this in resume instructions 
