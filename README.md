# Linux Networking Basic

## TCP/IP Protocol

### TCP (Transmission Control Protocol)

TCP/IP is the most popular networking protocol suite, is often referred to as a protocols, actually it's made up from several protocols. TCP and IP protocols, in addition there is also a third, named UDP.

1. TCP is responsible for breaking down network transmission into sequences (Packet and segment) which are sent to the target node and reassembled back into the original message.

2. TCP performs a three-way handshake , when setting up connection.

3. The first packet, SYN (synchronize), is sent to the receiver, that it wants to start a communication.

4. Once packet is received at the receiving end, a SYN/ACK (synchronize/acknowledge) packet is sent back to the sender.

5. Finally, an ACk (acknowledge) packet is sent to the receiver, and connection is established and the nods are able to communicate.

6. TCP has built-in features to deal with error, error correction ensure that a packet was received the same as, that was sent.

7. TCP packets contain a checksum and algorithm to verify it, if verification is fails, the packet is then discarded.

8. The flow controls feature in TCP handles the speed at which data is transferred. A transmission speed as fast as its slowest point in the path between two nodes.

9. Flow controls process is known as a sliding window, at receiving end receive window, which tells the sender that how much data it's able to receive.

## TFTP Server

### Introduction

This document will guide the reader on how to setup a TFTP server that will allow clients to both download and upload files. This process has been completely tested and verified on 18 Jun, 2021 using Ubuntu 20.04 LTS Server.

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
