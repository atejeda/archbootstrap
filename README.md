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

## Network (WiFi)

There's no preconfigured network, use iwd to configure the wifi connection if needed, some iwd hints:

List devices
```
iwctl device list
```

Scan networks
```
iwctl station DEVICE scan
```

Show networks
```
iwctl station DEVICE get-networks
```

Connect
```
iwctl station DEVICE connect SSID --passphrase PASSWORD
```

Check connection
```
iwctl station DEVICE show
```

DHCP configuration
```
dhclient
```

Check connection
```
ping 1.1.1.1.
```

Enable integrated DHCP (if needed)
```
cat <<EOF > /etc/iwd/main.conf
[General]
EnableNetworkConfiguration=true
EOF
```

Start iwd daemon (if necessary)
```
systemctl status iwd
systemctl start iwd
```

Configuration files
```
/var/lib/iwd/
```

More about iwd: https://wiki.archlinux.org/title/Iwd.

Check also: 
- https://wiki.archlinux.org/title/netctl
- https://wiki.archlinux.org/title/systemd-networkd
- https://wiki.archlinux.org/title/NetworkManager












