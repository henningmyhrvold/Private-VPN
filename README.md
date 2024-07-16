# Private VPN
Private Wireguard VPN. Always exit from your trusted home network, rather than untrusted VPN providers.


## Server Installation Steps:

### Disable root Bash history
```shell
echo "HISTFILESIZE=0" >> ~/.bashrc
history -c; history -w
source ~/.bashrc
```

### Disable root ssh login
```shell
sed -i -E 's/^(#)?PermitRootLogin (prohibit-password|yes)/PermitRootLogin no/' /etc/ssh/sshd_config
sed -i -E 's/^(#)?PasswordAuthentication yes/PasswordAuthentication no/' /etc/ssh/sshd_config
systemctl restart ssh
```

### Install Python, Pip & Ansible:
```shell
apt install python3 python3-pip pipx
pipx ensurepath
pipx install ansible
```

### Install Unattended Upgrades:
```shell
apt install unattended-upgrades
```

### Configure unnatended upgrades
vim /etc/apt/apt.conf.d/50unattended-upgrades and change the following:
```shell
Unattended-Upgrade::Remove-Unused-Kernel-Packages "true";
Unattended-Upgrade::Remove-Unused-Dependencies "true";
Unattended-Upgrade::Automatic-Reboot "true";
Unattended-Upgrade::Automatic-Reboot-WithUsers "true";
Unattended-Upgrade::Automatic-Reboot-Time "02:00";
```

### Activate unattended upgrades:
```shell
dpkg-reconfigure -plow unattended-upgrades
```

### Install Wireguard:
```shell
apt install wireguard
```

### Generate keys wg-server:
```shell
wg genkey | tee wg-server.key | wg pubkey > wg-server.pub
wg genpsk > peerA-B.psk
```


## Host Installation Steps:

### Generate keys wg-host:
```shell
wg genkey | tee wg-host.key | wg pubkey > wg-host.pub
```
