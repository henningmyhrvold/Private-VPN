# Private VPN
Private Wireguard VPN. Always exit from your trusted home network, rather than untrusted VPN providers.


## Installation Steps:
On both the endpoint client and the wg host

Install Unattended Upgrades:
```shell
apt install unattended-upgrades
```

vim /etc/apt/apt.conf.d/50unattended-upgrades and change the following:
```shell
Unattended-Upgrade::Remove-Unused-Kernel-Packages "true";
Unattended-Upgrade::Remove-Unused-Dependencies "true";
Unattended-Upgrade::Automatic-Reboot "true";
Unattended-Upgrade::Automatic-Reboot-WithUsers "true";
Unattended-Upgrade::Automatic-Reboot-Time "02:00";
```

Activate unattended upgrades:
```shell
dpkg-reconfigure -plow unattended-upgrades
```


Install Wireguard:
```shell
apt install wireguard
```

Generate keys endpoint-a:
```shell
wg genkey > endpoint-a.key
wg pubkey < endpoint-a.key > endpoint-a.pub
```

Generate keys host--b:
```shell
wg genkey > host-b.key
wg pubkey < host-b.key > host-b.pub
```
