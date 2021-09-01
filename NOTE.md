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

```bash
dokku apps:create api
dokku domains:add api api.example.com
dokku config:set --no-restart api KEY="MASTER_KEY"
dokku letsencrypt:enable api
```

```bash
git remote add dokku dokku@xx.xx.xxx.xxx:api #or git remote set-url dokku dokku@xx.xx.xxx.xxx:api
git push dokku master
```

### 4. Enable root login over SSH

```bash
nano /etc/ssh/sshd_config # vim /etc/ssh/sshd_config
# add PermitRootLogin yes
systemctl restart sshd
# or
service sshd restart

```

### 5. Change mirror ubuntu

```bash
sed -i "s/archive.ubuntu.com/mirrors.bkns.vn/g" /etc/apt/sources.list
```

### 6. AA installer

```bash
yum update -y && yum autoremove -y && yum clean all && reboot
yum install -y wget && wget -O install.sh http://www.aapanel.com/script/install_6.0_en.sh && bash install.sh aapanel
```

```bash
apt update -y && apt upgrade -y && apt autoremove -y && apt clean all && reboot
wget -O install.sh http://www.aapanel.com/script/install-ubuntu_6.0_en.sh && sudo bash install.sh aapanel
```

### 7. Update nameserver dns

```bash
echo "nameserver 1.1.1.1" >>  /etc/resolv.conf
echo "nameserver 1.0.0.1" >>  /etc/resolv.conf
```

### 8.

```bash
git config --system http.sslVerify false
git config --system user.email "email@email.com"
```

```
<IfModule mod_rewrite.c>
RewriteEngine On

RewriteRule .* - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization}]

RewriteBase /
RewriteRule ^index\.php$ - [L]

RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /index.php [L]
</IfModule>
```

```bash
/usr/local/lsws/admin/misc/lsup.sh -v 1.7.13
```
