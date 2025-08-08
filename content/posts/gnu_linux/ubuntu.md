
## Networking

Since Ubuntu 17 `netplan` was introduced to perform network configuration based on YAML files.

Netplan is an open source network configuration utility primarily used on Ubuntu and Debian based systems.

Netplan works on top of network managers like `NetworkManager` or `systemd-networkd` by rendering configuration for the network manager from YAMLs.

Netpla source code is on [netplan](https://github.com/canonical/netplan).

The main page for netplan is on: [https://netplan.io/](https://netplan.io/)

Examples:

Ethernet configuration example:

```yaml
# The YAML config files are located on: '/etc/netplan'
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: no
      addresses: [192.168.1.100/24]
      gateway4: 192.168.1.1
      nameservers:
        search: [itzgeek.local]
        addresses: [192.168.1.1,8.8.8.8]
```
WiFi example:
```yaml
network:
  version: 2
  renderer: NetworkManager
  wifis:
    wlx7c8bca0d69b6: # wifi interface name
      dhcp4: no
      addresses: [192.168.1.100/24]
      gateway4: 192.168.1.1
      nameservers:
        addresses: [192.168.1.1,8.8.8.8]
      access-points:
        Raj: # wifi ssid
          password: MyPass #wifi passwd
```
The config is generated with `netplan generate` and applied with `netplan apply`

To identify the interfaces available on the system run: `lshw -class network`.

To see the the network interface setting run: `ethtool eth4`, where `eth4` is the network interface name
