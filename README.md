# wireguard-deb
Private Wireguard VPN. Always exit from your trusted home network, rather than untrusted VPN providers.


## Installation Steps:
On both the endpoint client and the wg host

Install Wireguard:
```shell
$ apt install wireguard
```

Generate keys:
```shell
$ wg genkey > endpoint-a.key
$ wg pubkey < endpoint-a.key > endpoint-a.pub
$
$ wg genkey > host-b.key
$ wg pubkey < host-b.key > host-b.pub
```
