### 1. Delete all local git branches

```bash
git branch --merged | grep -v \* | xargs git branch -D 
```

### 2. Create swap for azure

Edit `/etc/waagent.conf`: 
```bash
ResourceDisk.Format=y                   # Format if unformatted. If 'n', resour$
ResourceDisk.Filesystem=ext4            # Typically ext3 or ext4. FreeBSD image$
ResourceDisk.MountPoint=/mnt/resource   #
ResourceDisk.EnableSwap=y               # Create and use swapfile on resource d$
ResourceDisk.SwapSizeMB=2048            # Size of the swapfile.
```

After that paste command: 
```bash
umount /mnt
service walinuxagent restart
```
