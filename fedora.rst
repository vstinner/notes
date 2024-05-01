.. _fedora:

++++++
Fedora
++++++

See also: :ref:`Python in Fedora <python-fedora>`.

Debuginfo
=========

To debug python3-cryptography, install debug symbols::

   sudo dnf debuginfo-install python3-cryptography


Download a source RPM
=====================

::

   sudo yum install yum-utils
   yumdownloader --source <package>
   # install build dependencies:
   yum-builddep python

You may have to enable "Source" repositories: see also
"yumdownloader --enablerepo=xxx" option.

Search a package without updating yum cache
===========================================

::

    yum search -C pattern

Which package provides the program route?
=========================================

::

    $ rpm -qf $(which route)
    net-tools-2.0-0.15.20131119git.fc20.x86_64

Or if the package is not installed::

    $ yum whatprovides route
    ...
    net-tools-2.0-0.15.20131119git.fc20.x86_64 : Basic networking tools
    ...
    Nom de fichier: /usr/sbin/route

Listing the files in a package
==============================

::

     rpm -ql mongodb-server

Install dependencies to build the package digikam
=================================================

::

    yum-builddep digikam

Packages
========

* https://apps.fedoraproject.org/packages/
* Example with gdb: https://apps.fedoraproject.org/packages/s/gdb
* https://koji.fedoraproject.org/koji/ : server where packages are built

Install manually a different version, package already installed:

   rpm -e gdb-8.2.50.20181010-5.fc30.x86_64.rpm

Rebuild a Fedora package
------------------------

Rebuild a package: `Fedora Source RPM <http://hacktux.com/fedora/source/rpm>`_.

If you get a .src.rpm package, you can rebuild it with::

    rpmbuild --rebuild wrk-3.1.0-1.fc21.src.rpm

Unpack RPM
----------

Unpack file.rpm in a new dir/ subdirectory::

    mkdir dir
    cp file.rpm dir/
    cd dir
    rpm2cpio file.rpm | cpio -idmv


sudo: add user to wheel group
=============================

::

   usermod -aG wheel vstinner

Python
======

* `Multiple Python interpreters
  <https://developer.fedoraproject.org/tech/languages/python/multiple-pythons.html>`_


Upgrade
=======

Upgrade Fedora 39 to Fedora 40 in command line::

    # sudo dnf upgrade --refresh
    sudo dnf install dnf-plugin-system-upgrade
    sudo dnf system-upgrade download --refresh --releasever=40 --allowerasing # --skip-broken
    sudo dnf system-upgrade reboot
    # at first boot on the new Fedora, fix SELinux labels:
    sudo fixfiles -B onboot
    # and reboot

Documentation: https://fedoraproject.org/wiki/DNF_system_upgrade

If the upgrade is interrupted for some reasons, attempt to repair it with::

    sudo dnf remove --duplicates --releasever=38 --allowerasing
    sudo dnf distrosync --releasever=38 --allowerasing
    sudo dnf reinstall "kernel*"


.. _abrt:

ABRT
====

See also :ref:`systemd coredumpctl <coredumpctl>`.

ABRT components
---------------

* /usr/bin/abrt-applet
* /usr/bin/abrt-dump-journal-core run by abrt-journal-core.service
* /usr/sbin/abrtd run by abrtd.service
* /usr/sbin/abrt-dbus run by DBus activation
* /usr/bin/abrt-dump-journal-oops run by abrt-oops.service

Ignore crashes in $HOME
-----------------------

Edit ``BlackListedPaths`` in ``/etc/abrt/abrt-action-save-package-data.conf``::

    $ sudo vim /etc/abrt/abrt-action-save-package-data.conf
    BlackListedPaths = (...), /home/vstinner/*

where ``(...)`` was the existing configuration. Full example::

    BlackListedPaths = /usr/share/doc/*, */example*, /usr/bin/nspluginviewer, /usr/lib*/firefox/plugin-container, /home/vstinner/*


Rawhide and GPG keys
====================

Rawhide: https://fedoraproject.org/wiki/Releases/Rawhide

GPG::

    $ rpm -qf /etc/pki/rpm-gpg/RPM-GPG-KEY-fedora-31-x86_64
    fedora-gpg-keys-31-0.2.noarch

Import Fedora's GPG key(s) (command comming from
https://getfedora.org/security/):

    curl https://getfedora.org/static/fedora.gpg | gpg --import

Last resort: disable gpgcheck in /etc/yum.repos.d/fedora-rawhide.repo (then reenable it).


List all packages installed on the system
==========================================

Using dnf::

    dnf history userinstalled

Using rpm::

    rpm -qa


dnf: file ... of xxx conflicts with file from package yyy
=========================================================

Attempt ``dnf remove xxx``.

If it's really not possible::

    dnf download yyy
    sudo rpm -ihv --force <downloaded RPM file>

RPM specfile
============

* ``%bcond_without rpmwheels`` enables rpmwheels feature (true)
* ``%bcond_with rpmwheels`` disables rpmwheels feature (false)


Change root password
====================

Official doc: https://docs.fedoraproject.org/en-US/quick-docs/reset-root-password/

* At boot, hold the CTRL key
* In GRUB, select the latest kernel with up/down keys, press "e", edit the
  "linux" line, add ``rw init=/bin/bash``, press CTRL+x or F10 to boot.
* In bash, type::

    # mount -o remount,rw /  # if you forgot rw
    # passwd
    <enter new root password here>
    # touch /.autorelabel
    # sync
    # /sbin/reboot -f

The ``touch /.autorelabel`` command recreate SELinux labels, especially
on the ``/etc/shadow`` file (label: ``system_u:object_r:shadow_t:s0``).
