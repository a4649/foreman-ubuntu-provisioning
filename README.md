# Provisioning Ubuntu 22 with The Foreman


## Create Installation media

#### Hosts > Installation Media > Create Medium

* Name: Ubuntu Mirror
* Path: http://archive.ubuntu.com/ubuntu
* Operating System Family: Debian

## Create Operating System

### Hosts > Operating Systems > Create Operating System

* Name: Ubuntu22
* Major version: 22.04
* Minor version: 05
* Description Ubuntu 22.04
* Family: Debian
* Release Name: jammy
* Architectures: x86_64

## Create Partition Table

* Hosts > Partition Tables > Create Partition Table:
* Name: cloud-init LVM
* Operating System Family: Debian
* Association > Ubuntu22
* Content: ubuntu22.ptable
* Change content inside <> to match your setup

## Create cloud-init tempalte

Hosts > Provisioning Templates > Create Template:
Name: Ubuntu22 cloud-init
Type: Provisioning template
Association > Ubuntu22
Content: ubuntu22.cloud-init

## Create Grub2 template

Hosts > Provisioning Templates > Create Template:
Name: Ubuntu22 cloud-init
Type: Provisioning template
Association > Ubuntu22
Content: ubuntu22.grub2
