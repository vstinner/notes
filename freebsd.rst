+++++++
FreeBSD
+++++++

Misc
====

* Coredump filename: ``sudo sysctl -w 'kern.corefile =%N.%P.core'``

Use FreeBSD
===========

* Rerun the installer configuration, run:: ``bsdconfig``.
* Change the keyboard layout: run ``kbdmap``.
* Upgrade to FreeBSD 12.0-RC1::

   $ sudo freebsd-update upgrade -r 12.0-RC1
   Does this look reasonable (y/n)? y
   $ sudo shutdown -r now
   $ sudo freebsd-update install

Upgrade
=======

Upgrade the system::

    sudo freebsd-update fetch
    sudo freebsd-update install
    pkg upgrade

Upgrade to FreeBSD 12.0-RC2::

   sudo freebsd-update fetch
   sudo freebsd-update upgrade -r 12.0
   sudo freebsd-update install
   sudo reboot
   # after reboot
   sudo freebsd-update install

Repair pkg, if needed::

   sudo pkg bootstrap -f

If something goes wrong, reinstall everything installed by pkg::

   sudo pkg-static upgrade -f


Install FreeBSD VM
==================

* https://www.freebsd.org/where.html : Download amd64/qcow2 virtual machine image,
* Uncompress the image: unxz file.qcow2.xz
* Move the image to /var/lib/libvirt/images/
* Create a FreeBSD VM using this disk image
* kbdcontrol -l fr.iso
* Log as root
* pkg install sudo bash screen vim-console
* adduser: add user, add it to the wheel group
* visudo: allow sudo for the whell group
* Unlog, log again as the new user
* chsh -s /usr/local/bin/bash
* Unlog, log again (to get bash)
* Enable the SSH server:

 * Add sshd_enable="YES" to /etc/rc.conf
 * service sshd start
 * https://www.freebsd.org/doc/handbook/openssh.html


Install FreeBSD CURRENT in a VM
===============================

* Download ftp://ftp.freebsd.org/pub/FreeBSD/releases/amd64/amd64/ISO-IMAGES/11.0/FreeBSD-11.0-RELEASE-amd64-disc1.iso.xz
* Uncompress: unxz FreeBSD-11.0-RELEASE-amd64-disc1.iso.xz
* Create a new VM:

  * Name: FreeBSD
  * Boot from an ISO: specify the path to the .iso file
  * System: select Show all, select UNIX, pick FreeBSD 11
  * 1 cpu, 1 GB of RAM
  * Disk size: 20 GB
  * Select network: shared interface, br0

* FreeBSD installer:


  * <install>
  * Keymap: French ISO-8859-1
  * Hostname: freebsd
  * Distribution: only keep [*] ports
  * Partition: auto, <Entire disk>, MBR, Finish, Commit
  * (choose a root password)
  * network: configure IPv4, use DHCP, yes, configure IPv6, auto, yes
  * Time Zone: 8 Europe, 14 France
  * Date/Time: Skip
  * Service started at boot: sshd
  * (no option)
  * Add a new user: username vstinner
  * Exit: Manual config? No
  * Reboot

* (After reboot)
* Log as root
* type "pkg install sudo" and install it
* run "visudo" and uncomment "%whell ALL.." without password
* add vstinner user to the wheel group: pw group mod wheel -m vstinner
* Relog as vstinner
* sudo pkg install bash git
* chsh: write /usr/local/bin/bash (check before with "which bash")
* Delog, log again as vstinner
