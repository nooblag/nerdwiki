### One-liner to purge old kernels

Thanks [@captainmish](https://askubuntu.com/a/1417955)

```
dpkg -l | egrep -i 'linux-image|linux-headers|linux-modules' | grep -v $(uname -r) | awk '{ print $2 }' | xargs sudo apt purge -y
```

