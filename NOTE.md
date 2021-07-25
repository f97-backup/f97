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

### 3. Play with dokku

```bash
wget https://raw.githubusercontent.com/dokku/dokku/v0.24.10/bootstrap.sh;
sudo DOKKU_TAG=v0.24.10 bash bootstrap.sh
```

```bash
ssh-keygen -t rsa -b 4096 
cat ~/.ssh/id_rsa.pub # And paste text to http://<IP>
```

```
dokku apps:create api
domains:add api api.example.com
dokku config:set --no-restart api KEY="MASTER_KEY"
dokku letsencrypt:enable api
```
```
git remote add dokku dokku@xx.xx.xxx.xxx:api
git push dokku master
```
