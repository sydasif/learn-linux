Go to sudo vi /etc/netplan/00-installer-config.yaml

(ubuntu server 20.04 LTS)

# This is the network config written by 'subiquity'
network:
  ethernets:
    ens33:
      addresses:
      - 10.1.1.200/24
      dhcp4: false
      gateway4: 10.1.1.1
      nameservers:
        addresses:
        - 8.8.8.8
        - 192.168.8.2
        search:
        - workgroup
    ens34:
      dhcp4: true
  version: 2