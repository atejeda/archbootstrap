# archbootstrap

An ArchLinux bootstrap scripts.

The repository consists of a configuration file and two scripts:

## environment

A bash file used as a configuration file.

## 00.step.sh

It wipes out the specified disk in the configuration file (environment, in which
creates two partitions, one for boot and other for the OS.

The OS partition is encrypted with crypsetup and configured with a
basic LVM layout with ext4 as the filesystem.

After the disk has been configured, it generates a environment.partition file
to be used by the 01.script.sh (needed to configure and setup grub).

## 01.step.sh

It does some local and locale configuration, setting up the hostname, resolv, 
passwords, users, sudoers and grub configuration (only EFI is being supported for now).

Finally allocating swap as a file.

## Caveats

There's no preconfigured network, use iwd to configure the wifi connection if needed, some iwd hints:


```
# list devices
iwctl device list

# scan
iwctl station DEVICE scan

# show networks
iwctl station DEVICE get-networks

# connect
iwctl station DEVICE connect SSID --passphrase PASSWORD

# check connection
iwctl station DEVICE show

# dhcp configuration if needed
dhclient

# test network
ping 1.1.1.1.

# enable integrated dhcp
cat <<EOF > /etc/iwd/main.conf
[General]
EnableNetworkConfiguration=true
EOF

# start daemon if necessary
systemctl status iwd
systemctl start iwd

# network configuration files
/var/lib/iwd/
```
















