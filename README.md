# ScaleIO_VirtualBox
Creating an install of ScaleIO on VirtualBox for labs and light testing

## Introduction

### SYSTEM REQUIREMENTS
 
ScaleIO Linux

RAM

500 MB RAM for the MDM and each SDS. 50 MB RAM for each SDC

OS

Linux RHEL or CentOS 6 or 7, Ubuntu 14.04 or 16.04, SUSE 11 SP3,SUSE 12, or SUSE 12 SP1

Hardware

Intel or AMD x86 64-bit

Virtual infrastructure

Red Hat KVM, XenServer 6.5, 7.0

### Layout

3 Servers for MDM, 500 MB RAM

3 Servers for SDS, 500 MB RAM
 
1 Server for SDC, 500 MB Ram



### Software Download
 
https://emcinformation.com/483301/REG/.ashx

Plase this in the working directory, I can not add it to the git repository.

### Vagrant update

We need to install the vagrant-disksize addon to make room for the SDS servers

```
vagrant plugin install vagrant-disksize
Installing the 'vagrant-disksize' plugin. This can take a few minutes...
Fetching: vagrant-disksize-0.1.2.gem (100%)
Installed the plugin 'vagrant-disksize (0.1.2)'!
```

