+++++++
FreeBSD
+++++++

Upgrade
=======

Check the `latest FreeBSD release <https://www.freebsd.org/>`_ and compare to
``uname -a``.

Upgrade the system::

    sudo pkg upgrade -y
    sudo bash -c 'PAGER=cat freebsd-update fetch'
    sudo bash -c 'PAGER=cat freebsd-update install'

``PAGER=cat`` is used to ignore messages about added, removed and overriden
configuration files.

Minimum packages to develop on FreeBSD
======================================

Install::

    pkg  # first command proposes to install it
    pkg install sudo
    sudo pkg install vim-console git

Misc
====

* Coredump filename: ``sudo sysctl -w 'kern.corefile =%N.%P.core'``

Configuration
=============

* Rerun the installer configuration, run:: ``bsdconfig``.
* Change the keyboard layout: run ``kbdmap``.


Upgrade to newer FreeBSD
========================

Upgrade to FreeBSD 12.0-RC2::

   sudo freebsd-update fetch
   sudo freebsd-update upgrade -r 12.0
   sudo freebsd-update install
   sudo reboot
   # after reboot
   sudo freebsd-update install


Repair pkg
==========

Repair pkg, if needed::

   sudo pkg bootstrap -f

If something goes wrong, reinstall everything installed by pkg::

   sudo pkg-static upgrade -f


Install FreeBSD VM
==================

Install VM image
----------------

* https://www.freebsd.org/where.html : Download amd64/qcow2 virtual machine image,
* Uncompress the image: unxz file.qcow2.xz
* Move the image to /var/lib/libvirt/images/
* Create a FreeBSD VM using this disk image
* Add "freebsd" hostname to /etc/hosts

Classic installer (old way)
---------------------------

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

Enlarge qcow2 image
-------------------

* Shutdown the VM
* On the host: sudo qemu-img resize /var/lib/libvirt/images/freebsd.qcow2 40G
* Boot the VM, in FreeBSD: sudo /etc/rc.d/growfs onestart

Configure as root
-----------------

* Log as root
* ``kbdcontrol -l fr.iso``
* ``pkg install sudo bash tmux vim``
* ``visudo``: uncomment ``%whell ALL..`` without password
* adduser: add user, add it to the wheel group
* to add wheel group to an user: pw usermod -n vstinner -G wheel
* Enable the SSH server:

 * Add sshd_enable="YES" to /etc/rc.conf
 * service sshd start
 * https://www.freebsd.org/doc/handbook/openssh.html

* Log out

Configure as your user
----------------------

* Log in as the your user
* chsh -s /usr/local/bin/bash
* Log out and log in again to get bash
* ``sudo pkg install git``

Commands to develop Python on FreeBSD
=====================================

Install::

    sudo pkg install pkgconf

Use ports
=========

By default, ports are not installed::

    vstinner@freebsd$ ls /usr/ports
    ls: /usr/ports: No such file or directory

Install ports::

    sudo git clone https://git.FreeBSD.org/ports.git /usr/ports --depth=1

Misc
====

Which package provides a file? ::

    vstinner@freebsd$ pkg which /usr/local/bin/git
    /usr/local/bin/git was installed by package git-2.41.0

FreeBSD source code: https://github.com/freebsd/freebsd-src/

DHCP error
==========

* https://forums.freebsd.org/threads/fresh-freebsd-14-1-guest-vm-does-not-receive-any-dhcpoffers.95189/#post-674508
* https://lists.libvirt.org/archives/list/users@lists.libvirt.org/thread/DJFOKQ7RDPAOFGUJZYY56TJTORHHQKWI/
* https://www.spinics.net/linux/fedora/libvir/msg249203.html

fix_network.sh::

    set -x -e
    ifconfig vtnet0 -rxcsum -txcsum
    service dhclient restart vtnet0
