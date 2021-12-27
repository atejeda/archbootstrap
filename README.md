# archbootstrap

An ArchLinux bootstrap scripts.

The repository consists of a configuration file and two scripts:

## environment

A bash file used as a configuration file.

## 00.step.sh

It wipes out the specified disk in the configuration file (environment_, in which
creates two partitions, one for boot and other for the OS.

The OS partition is encrypted with crypsetup and configured with a
basic LVM layout with ext4 as the filesystem.

After the disk has been configured, it generates a environment.partition file
to be used by the 01.script.sh (needed to configure and setup grub).

## 01.step.sh

It does some local and locale configuration, setting up the hostname, resolv, 
passwords, users, sudoers and grub configuration (only EFI is being supported for now).

Finally allocating swap as a file.
