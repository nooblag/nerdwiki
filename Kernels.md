### One-liner to purge old kernels

Thanks [@captainmish](https://askubuntu.com/a/1417955)

```
dpkg -l | egrep -i 'linux-image|linux-headers|linux-modules' | grep -v $(uname -r) | awk '{ print $2 }' | xargs sudo apt purge -y
```

More cautious/verbose:

```
dpkg --list |
  grep --ignore-case --extended-regexp 'linux-image|linux-headers|linux-modules' |
  grep --invert-match "$(uname --kernel-release)" |
  awk '{ print $2 }' |
  xargs sudo apt purge
```
