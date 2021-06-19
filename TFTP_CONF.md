# TFTP Server

### Introduction

This document will guide the reader on how to setup a TFTP server that will allow clients to both download and upload files.

This process has been completely tested and verified on 18 Jun, 2021 using Ubuntu 20.04 LTS Server.

### Installation

*sudo apt-get install tftpd-hpa*

You can confirm this by running...

*sudo service tftpd-hpa status*

### Configuration

Edit the tftpd-hpa configuration file.

*sudo vi /etc/default/tftpd-hpa*

TFTP_OPTIONS="--secure --create"

Save the file and exit the vi editor

Modify Permissions on TFTP Root Directory

*sudo chown -R tftp /srv/tftp*

Restart the tftpd-hpa Service

*sudo service tftpd-hpa restart*

[External Links](https://help.ubuntu.com/community/TFTP)
