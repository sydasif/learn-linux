# Linux Networking Lab

## TFTP Server

### Introduction

This document will guide the reader on how to setup a TFTP server that will allow clients to both download and upload files.
This process has been completely tested and verified on 18 Jun, 2021 using Ubuntu 20.04 LTS Server.

### Installation

`sudo apt-get install tftpd-hpa`

You can confirm this by running...

`sudo service tftpd-hpa status`

### Configuration

Edit the tftpd-hpa configuration file.

`sudo vi /etc/default/tftpd-hpa`

Replaced __TFTP_OPTIONS__ with line below

`TFTP_OPTIONS="--secure --create"`

Save the file and exit the editor

### Modify Permissions on TFTP Root Directory

`sudo chown -R tftp /srv/tftp`

Restart the tftpd-hpa Service

`sudo service tftpd-hpa restart`

[__External Links:__](https://help.ubuntu.com/community/TFTP)

## DNS

### [dnsmasq](https://thekelleys.org.uk/dnsmasq/doc.html)

### Setting of DNS

Since Ubuntu 18.04 ships with systemd-resolved by default (and it's bound to port 53), you'll want to perform a few extra steps:

First,  disable and stop systemd-resolved:

`sudo systemctl disable systemd-resolved`

`sudo systemctl stop systemd-resolved`

Second, delete the existing /etc/resolv.conf file, as it's a symlink to ../run/systemd/resolve/stub-resolv.conf

`sudo rm /etc/resolv.conf`

Create a new /etc/resolv.conf file with this:

`echo "nameserver 8.8.8.8" > /etc/resolv.conf`

Install dnsmasq:

`sudo apt-get install dnsmasq`

After install, the /etc/dnsmasq.conf file should be present.  After any changes, you'll need to restart the service:

`sudo systemctl restart dnsmasq`

If you want to keep both dnsmasq and the systemd-resolved stub-resolver enabled and running, 

there are some ways to do that listed [HERE](https://unix.stackexchange.com/questions/304050/how-to-avoid-conflicts-between-dnsmasq-and-systemd-resolved).

### Configuration

**Go to `sudo vi /etc/dnsmasq.conf`**

uncommit line below:

`domain-needed`

`bogus-priv`

**Add line below:**

`local=/home.com/`

**Add line below:**

`address=/r1/10.1.1.1`

`address=/server/10.1.1.200`

`address=/ubuntu-1/10.1.1.201`


## DHCP

### Configuration

**Go to `sudo vi /etc/dnsmasq.conf`**

Add line below:

**to set dhcp range**

`dhcp-rnage=10.1.1.150,10.1.1.199,255.255.255.0,24h` 

**to set default gateway**

`dhcp-optinon=3,10.1.1.1`
