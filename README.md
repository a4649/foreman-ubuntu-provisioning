# Provisioning Ubuntu 22 with The Foreman


## Create Installation media

#### Hosts > Installation Media > Create Medium

* Name: Ubuntu Mirror
* Path: http://archive.ubuntu.com/ubuntu
* Operating System Family: Debian

## Create Operating System

#### Hosts > Operating Systems > Create Operating System

* Name: Ubuntu22
* Major version: 22.04
* Minor version: 3
* Description Ubuntu 22.04
* Family: Debian
* Release Name: jammy
* Architectures: x86_64

## Create Partition Table

#### Hosts > Partition Tables > Create Partition Table:

* Name: cloud-init LVM
* Operating System Family: Debian
* Association > Ubuntu22
* Content: ubuntu22.ptable
* NOTE: only works for nvme disk. For sata replace 'nvme0n1' with 'sda'

## Create cloud-init tempalte

#### Hosts > Provisioning Templates > Create Template:

* Name: Ubuntu22 cloud-init
* Type: Provisioning template
* Association > Ubuntu22
* Content: ubuntu22.cloud-init

## Create Grub2 template

#### Hosts > Provisioning Templates > Create Template:

* Name: Ubuntu22 cloud-init
* Type: Provisioning template
* Association > Ubuntu22
* Content: ubuntu22.grub2
* Change content inside <> to match your setup

## Kernel and Initrd

Download Ubuntu ISO and extract kernel and initrd

```wget https://releases.ubuntu.com/22.04.3/ubuntu-22.04.3-live-server-amd64.iso``` 

```mkdir /mnt/ubuntu```

```mkdir /var/lib/tftpboot/boot/ubuntu22```

```mount ubuntu-22.04.3-live-server-amd64.iso /mnt/ubuntu```

```cp /mnt/ubuntu22/casper/vmlinuz /var/lib/tftpboot/boot/ubuntu22/```

```cp /mnt/ubuntu22/casper/initrd /var/lib/tftpboot/boot/ubuntu22/```

## Make the ISO available in the network

In my case I have different Operating Systems to provision with Foreman, for that I have a virtual machine with the intallation ISO's.

```dnf install -y httpd```
```systemctl enable --now httpd```
```mkdir -p /var/www/html/pub/ubuntu22```
```cp ubuntu-22.04.3-live-server-amd64.iso /var/www/html/pub/ubuntu22/```
