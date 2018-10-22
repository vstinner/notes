++++++
Fedora
++++++

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
