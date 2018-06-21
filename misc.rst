++++++++++++++
Unsorted Notes
++++++++++++++

.. image:: great_flamingo.jpg
   :alt: Great Flamingo
   :align: right
   :target: http://www.flickr.com/photos/haypo/11915292626/

GitHub
======

Fedora::

    sudo dnf install -y hub

Download a pull request::

    git checkout -b pr104
    git am -3 https://github.com/python/cpython/pull/104

URLs:

* Add ``?w=1`` in a pull request to ignore whitespace changes
* Add ``.patch`` to a pull request to get the change as an unified diff
* In a message, ``<details> ... </details>`` creates a drop-down

vim for developer
=================

In these examples, I'm using Mercurial with the command "hg". To use git, just
replace "hg" with "git". I prefer the graphical editor gvim. To use the console
version, replace "gvim" with "vim".

View differences::

    hg diff | gvim -

Shortcuts:

* ``a/asyncio/events.py``: to open the file, delete ``a\``, put the cursor
  on the file type, type ``vs`` for a vertial split, and type ``gf`` (goto
  file) to open the file
* ``%bd``: close all buffers

Python:

* ``[[``, ``]]``: jump to previous/next of the class or fnuction



Fedora
======

Search a package without updating yum cache::

    yum search -C pattern

Which package provides the program route? ::

    $ rpm -qf $(which route)
    net-tools-2.0-0.15.20131119git.fc20.x86_64

Or if the package is not installed::

    $ yum whatprovides route
    ...
    net-tools-2.0-0.15.20131119git.fc20.x86_64 : Basic networking tools
    ...
    Nom de fichier: /usr/sbin/route

Listing the files in a package::

     rpm -ql mongodb-server

Install dependencies to build the package digikam::

    yum-builddep digikam

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


Code search
===========

* https://github.com/search/
* http://searchcode.com/
* https://codesearch.debian.net/
* http://stackoverflow.com/search?q=codecs.encode
* specific to OpenStack: http://codesearch.openstack.org/


Git
===

Remove latest commit
--------------------

::

    git reset --hard HEAD~1

List tags containing a specific commit
--------------------------------------

::

    nova$ git tag --contains 94a3b83f9f1fd52a78b9d49b32ddfae40182f852
    12.0.0.0b1
    12.0.0a0
    2014.2
    2014.2.1
    2014.2.2
    2014.2.3
    2014.2.b1
    2014.2.b2
    2014.2.b3
    2014.2.rc1
    2014.2.rc2
    2015.1.0
    2015.1.0b1
    2015.1.0b2
    2015.1.0b3
    2015.1.0rc1
    2015.1.0rc2
    2015.1.0rc3


Remote branches
---------------

* List remote branches: ``git branch -r``
* Create a new branch ``fix_1369426_icehouse`` tracking the remote branch
  ``origin/stable/icehouse``::

    git branch --track fix_1369426_icehouse origin/stable/icehouse

* (Track and) Pull a remote branch::

    git branch --track NAME_REMOTE_BRANCH
    git fetch --all   # or: git pull --all

Send email
----------

First install ``git send-email``. On Fedora::

    yum install -y git-email

Generate a .patch file for a single commit::

    git format-patch origin/master

Generate a patch serie for multiple commits::

    git format-patch origin/master --cover-letter

Now modify ``0000-cover-letter.patch``: replace ``*** BLURB HERE ***``. By
default, patches create a thread on a mailing list: ``[PATCH 0/n]`` is the top
message, ``[PATCH 1/n]``, ``[PATCH 2/n]``, etc. are replied to the top message.
See ``Message-Id`` and ``In-Reply-To`` headers in emails.

To generate a version 2 of a patch (use ``[PATCH v2]`` subject prefix instead
of ``[PATCH]``)::

    git format-patch origin/master --subject-prefix 'PATCH v2'

Send patches::

    git send-email --to=EMAIL --suppress-cc=all *.patch

For your first try, just send emails to yourself ;-)


OpenStreetMap
=============

Map of the town Peypin:

* `OpenStreetMap <http://www.openstreetmap.org/relation/93723>`_
* `Google Maps <https://maps.google.com/maps?ll=43.384146,5.577428&spn=0.005544,0.013368&sll=37.0625,-95.677068&sspn=49.089956,109.511719>`_
* `Yahoo Maps <https://maps.yahoo.com/place/?lat=43.38477800510547&lon=5.580840110778809&bb=43.391405312706%2C5.564478635787964%2C43.37816556912287%2C5.597201585769653&addr=Peypin%2C France>`_
* `OSMOSE <http://osmose.openstreetmap.fr/fr/map/#zoom=15&lat=43.38312&lon=5.57648&layer=Mapnik&overlays=FFFFFFFFFFFFFFFFFFFT&item=xxxx&level=1%2C2%2C3&tags=&fixable=&bbox=0.1373291015625%2C42.53689200787317%2C7.0751953125%2C45.98169518512228>`_
* `BANO <http://layers.openstreetmap.fr/?zoom=16&lat=43.38333&lon=5.5835&layers=B0000FFFFFFFFFFFFFFFFFFFFFFT>`__
* `KeepItRight <http://keepright.at/report_map.php?lang=fr&ch30=1&ch40=1&ch50=1&ch70=1&ch90=1&ch100=1&ch110=1&ch120=1&ch130=1&ch150=1&ch160=1&ch170=1&ch180=1&ch191=1&ch192=1&ch193=1&ch194=1&ch195=1&ch196=1&ch197=1&ch198=1&ch201=1&ch202=1&ch203=1&ch204=1&ch205=1&ch206=1&ch207=1&ch208=1&ch210=1&ch220=1&ch231=1&ch232=1&ch270=1&ch281=1&ch282=1&ch283=1&ch284=1&ch285=1&ch291=1&ch292=1&ch293=1&ch294=1&ch295=1&ch296=1&ch297=1&ch298=1&ch311=1&ch312=1&ch313=1&ch320=1&ch350=1&ch370=1&ch380=1&ch401=1&ch402=1&ch411=1&ch412=1&ch413=1&number_of_tristate_checkboxes=8&highlight_error_id=0&highlight_schema=0&lat=43.38304&lon=5.57771&zoom=16&show_ign=1&show_tmpign=1&layers=B0T&ch=0%2C30%2C40%2C50%2C70%2C90%2C100%2C110%2C120%2C130%2C150%2C160%2C170%2C180%2C191%2C192%2C193%2C194%2C195%2C196%2C197%2C198%2C201%2C202%2C203%2C204%2C205%2C206%2C207%2C208%2C210%2C220%2C231%2C232%2C270%2C281%2C282%2C283%2C284%2C285%2C291%2C292%2C293%2C294%2C295%2C296%2C297%2C298%2C311%2C312%2C313%2C320%2C350%2C370%2C380%2C401%2C402%2C411%2C412%2C413>`_
* `viamichelin <http://www.viamichelin.fr/web/Cartes-plans/Carte_plan-Peypin-13124-Bouches_du_Rhone-France-D46A?strLocid=35MTE1NHRhajA2MjdldzF5NjMyaGtuYTQyOTljMTAyMnNjTkRNdU16ZzBNems9Y05TNDFOemMyTnc9PQ==&loc=no&layers=00000001&zoomLevel=12&strCoord=5.57767*43.38439>`_
* `Cadastre <http://www.cadastre.gouv.fr/scpc/afficherCarteCommune.do?c=80073&dontSaveLastForward&keepVolatileSession=>`_

Marseille user group:

* https://wiki.openstreetmap.org/wiki/Marseille#Rencontres_mensuelles
* https://wiki.openstreetmap.org/wiki/Marseille/R%C3%A9unions_2014
* http://listes.openstreetmap.fr/wws/info/local-marseille

Wiki:

* http://wiki.openstreetmap.org/wiki/FR:Quality_assurance
* http://wiki.openstreetmap.org/wiki/FR:Map_Features
* `BANO <http://wiki.openstreetmap.org/wiki/WikiProject_France/WikiProject_Base_Adresses_Nationale_Ouverte_(BANO)>`__


Shell script
============

* `bash8 <https://pypi.python.org/pypi/bash8>`_: A pep8 equivalent for bash
  scripts
* `checkbashisms <http://freecode.com/projects/checkbashisms>`_: static
  analysis tool for shell scripts. It looks for particular patterns which
  indicate a script might be relying on /bin/sh being bash.
* `shellcheck <http://www.shellcheck.net/>`_: static analysis and linting tool
  for sh/bash scripts
* ``$'...'`` interprets escape sequences (like ``\n``) in ``'...'``

Example::

    haypo@selma$ echo $'a\rb'|hexdump -C
    00000000  61 0d 62 0a                                       |a.b.|
    00000004

Ftrace
======

* LWN articles:

  - `Secrets of the Ftrace function tracer <http://lwn.net/Articles/370423/>`_
  - `Debugging the kernel using Ftrace - part 1 <http://lwn.net/Articles/365835/>`_
  - `A look at ftrace <http://lwn.net/Articles/322666/>`_
  - `Debugging the kernel using Ftrace - part 2 <http://lwn.net/Articles/366796/>`_
  - `Ftrace: The hidden light switch <http://lwn.net/Articles/608497/>`_

* `ftrace - Function Tracer
  <https://www.kernel.org/doc/Documentation/trace/ftrace.txt>`_: official
  documentation from the kernel
* `ftrace at elinux.org <http://elinux.org/Ftrace>`_
* `Kernel dynamic memory analysis <http://elinux.org/Kernel_dynamic_memory_analysis>`_
* `Installing and Using Ftrace <http://omappedia.org/wiki/Installing_and_Using_Ftrace>`_


Mercurial
=========

.. _hg-bisect:

bisect with a command
---------------------

Shell script ``cmd.sh``::

    set -e -x
    make
    ./python script.py

where ``script.py`` is the script to reproduce the bug.

Cleanup everything::

    hg bisect --reset
    hg update -C

We know that the most recent version is bad (``./cmd`` fails)::

    ./cmd.sh
    # cmd.sh failed
    hg bisect -b

Find a good revision using a date::

    hg up -r "branch(default) and date('May 2015')"
    ./cmd.sh
    # it's still failing, take an older date
    hg up -r "branch(default) and date('Jan 2015')"
    ./cmd.sh
    # iterate until the test pass
    (...)
    hg bisect -g

Ok, we have a good and a bad revision, and a script to automate the bisection::

    hg bisect --command ./cmd.sh
    # enjoy watching your computer working for you


cannot edit immutable changeset: xxx
------------------------------------

You can force the phase of a changeset back to draft like so::

    hg phase -d -f <changeset_id>

Only do that for private changes!


Find tags containing a specific changeset
-----------------------------------------

Let's say that you want to check which versions contains the _FUTURE_CLASSES
variable::

    $ grep '_FUTURE_CLASSES =' trollius/*.py
    trollius/futures.py:    _FUTURE_CLASSES = (Future, events.asyncio.Future)
    trollius/futures.py:    _FUTURE_CLASSES = Future

    $ hg blame trollius/futures.py|grep '_FUTURE_CLASSES ='
    1712:     _FUTURE_CLASSES = (Future, events.asyncio.Future)
    1688:     _FUTURE_CLASSES = Future

    $ hg log -r 1688 --template '{date|isodate}\n'
    2014-07-25 10:05 +0200

Ok, so the _FUTURE_CLASSES was added by the changeset ``1688`` which was made
the 2014-07-25. We pick the oldest changeset, ``1712`` was probably a fix.

Find the tags which contains the changeset ``1688``::

    $ hg log -r "reverse(descendants(1688)) and tag()" --template "{tags}\t{rev}:{node|short}\n"
    trollius-1.0.2  1767:41ac07cd2d03
    trollius-1.0.1  1738:83e574a42e16

    $ hg log -r trollius-1.0.1 --template '{date|isodate}\n'
    2014-07-30 17:45 +0200
    $ hg log -r trollius-1.0.2 --template '{date|isodate}\n'
    2014-10-02 16:47 +0200

The _FUTURE_CLASSES was introduced in trollius-1.0.1 which was released the
2014-07-30.  The following release trollius-1.0.2 (2014-10-02) also contains
it, which is expected since trollius-1.0.2 is based on trollius-1.0.1.

Check versions::

    $ hg up trollius-1.0.1
    $ grep '_FUTURE_CLASSES =' trollius/*.py
    trollius/futures.py:    _FUTURE_CLASSES = (Future, events.asyncio.Future)
    trollius/futures.py:    _FUTURE_CLASSES = Future

    $ hg up trollius-1.0
    $ grep '_FUTURE_CLASSES =' trollius/*.py
    trollius/tasks.py:    _FUTURE_CLASSES = (futures.Future, asyncio.Future)
    trollius/tasks.py:    _FUTURE_CLASSES = futures.Future

Ok, so in fact the variable was moved from the Python module ``trollius.tasks``
to the modle ``trollius.futures`` between versions 1.0 and 1.0.1.

abort: can't rebase public changeset fb6b735060b5
-------------------------------------------------

Error::

    abort: can't rebase public changeset fb6b735060b5
    (see "hg help phases" for details)


Misc
====

* `Linux: detect launching of programs <https://stackoverflow.com/questions/6075013/linux-detect-launching-of-programs>`_ (StackOverflow)
* `MLVPN - MultiLink Virtual Public Network <http://www.mlvpn.fr/>`_
* Docker: https://linuxfr.org/news/docker-tutoriel-pour-manipuler-les-conteneurs
* `Forensically <https://29a.ch/photo-forensics/>`_: tools to check if a photo
  was modified
* PHP: http://blog.mageekbox.net/


Share files files from Linux to OSX
===================================

I tried NFS: issues with non-ASCII characters, issue with Unicode NFC
normalization on OS X. Since OS X 10.9, the only way is to use the command line
to pass the option ``-o nfc`` to ``mount -t nfs ...``.

I tried Samba: well, it's not easy. Let's say that the directory to share is
``/data``.

Prepare permissions, readable by everybody, UNIX and SELinux permissions::

    sudo find  /data -type f -print0|xargs -0 chmod 644
    sudo find -type d -print0|xargs -0 chmod 755
    sudo semanage fcontext -a -t samba_share_t "/data(/.*)?"
    sudo restorecon -R -v data/

Install Samba::

    sudo yum install samba samba-common samba-client cups-lib system-config-samba

Use ``system-config-samba`` to share ``/data``:

* run ``sudo system-config-samba``
* add ``/data`` directory as ``public`` and make it readable for everybody
* add a Windows user which is binded to your user (Preference, Samba users)

Start Samba server and run it at boot::

    sudo systemctl start smb.service
    sudo systemctl start nmb.service
    sudo systemctl enable smb.service
    sudo systemctl enable nmb.service

Mac OS X:

* Finder, Go, Access server: use ``smb://192.168.0.1/data`` URL
* Type the user and password
* Enjoy!

Very good tutorial for Fedora 20:  `How to enable samba share for a specific
directory - Fedora 20
<https://ask.fedoraproject.org/en/question/40353/how-to-enable-samba-share-for-a-specific-directory-fedora-20/>`_.


Friends
=======

* http://blog.sileht.net/
* http://www.florentflament.com/
* http://yeknan.free.fr/dc2/

Fun:

* http://tumourrasmoinsbete.blogspot.fr/
* http://www.commitlogsfromlastnight.com/


systemd
=======

list servers
------------

Find the name of the systemd unit for MariaDB or RabbitMQ server.

List all installed services, including disabled services, and search for "maria"::

    systemctl list-unit-files --type=service | grep maria

Alternative if you know the package::

    $ rpm -ql mariadb-server|grep service
    /usr/lib/systemd/system/mariadb.service

List enabled services::

    systemctl list-units

Note: it looks like "list-units" doesn't show mariadb.service, probably because
it is disabled (not started at boot).


system logs (syslogs), journald
-------------------------------

* Show syslog from the most recent to the oldest logs: ``journalctl --reverse``
* Show all logs since the last boot: ``journalctl -b 0``
* List boots: ``journalctl --list-boots``
* ``tail -f /var/log/syslog``: ``journalctl -f``
* ``tail -f /var/log/syslog`` but only for apache: ``journalctl -u apache.service -f``


getaddrinfo
===========

* `A surprising discovery on converting IPv6 addresses: we no longer prefer
  getaddrinfo()
  <http://blog.powerdns.com/2014/05/21/a-surprising-discovery-on-converting-ipv6-addresses-we-no-longer-prefer-getaddrinfo/>`_
  (PowerDNS blog,  May 2014)
* glibc 2.15 (March 2012):
  `Avoid __check_pf calls in getaddrinfo unless really needed
  <https://sourceware.org/git/?p=glibc.git;a=commit;h=fa3fc0fe5f452d0aa7e435d8f32e992958683819>`_
* `Python issue: getaddrinfo is wrongly considered thread safe on linux
  <https://bugs.python.org/issue21216>`_
* `libc6: getaddrinfo() sends DNS queries to random file descriptors
  (CVE-2013-7423) <https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=722075>`_
  (glibc 2.13, fixed at least in glibc 2.19)


PostgreSQL
==========

Install PostgreSQL server on Fedora 21. Type as root::

    yum install postgresql-server
    postgresql-setup initdb

Modify ``/var/lib/pgsql/data/postgresql.conf`` to accept connections from
192.168.0.0/24 network, replace::

    #listen_addresses = 'localhost'         # what IP address(es) to listen on;
    ...
    max_connections = 100                  # (change requires restart)


with::

    listen_addresses = '*'
    ...
    max_connections = 1000                  # (change requires restart)

Modify ``/var/lib/pgsql/data/pg_hba.conf`` to allow login using a password from
192.168.0.0/24 network, replace::

    host    all             all             127.0.0.1/32            ident

with::

    host    all             all             192.168.0.0/24          md5

Start PostgreSQL::

    systemctl start postgresql


Switch to the ``postgres`` user (``sudo -u postgres -H -s``), open the psql
client (``psql``) and type::

    CREATE USER bigdata;
    ALTER ROLE bigdata WITH CREATEDB;
    ALTER USER bigdata WITH ENCRYPTED PASSWORD 'password';
    CREATE DATABASE bigdata;

* http://doc.fedora-fr.org/wiki/Installation_et_configuration_de_PostgreSQL


Google
======

What Google knowns on you:

* https://myactivity.google.com/
* https://myaccount.google.com/
* https://maps.google.fr/locationhistory/


.. _operating-systems:

Operating systems
=================

.. _macos-list:

`macOS (Mac OS X) versions
<https://en.wikipedia.org/wiki/macOS#Release_history>`_:

==============  ============== ==============  ============
macOS           Name           Darwin Version  Release Year
==============  ============== ==============  ============
macOS 10.13     High Sierra    17.x            2017 (June)
macOS 10.12     Sierra         16.x            2016
macOS 10.11     El Capitan     15.x            2015
macOS 10.10     Yosemite       14.x            2014
macOS 10.9      Mavericks      13.x            2013
macOS 10.8      Mountain Lion  12.x            2012
macOS 10.7      Lion           11.x            2010
macOS 10.6      Snow Leopard   10.x            2008
macOS 10.5      Leopard        9.x             2006
macOS 10.4      Tiger          8.x             2004
==============  ============== ==============  ============

* `Linux kernel versions
  <https://en.wikipedia.org/wiki/Linux_kernel#Maintenance>`_:

  - 4.0: 2015 (under development)
  - 3.0: 2011
  - 2.6: 2003
  - 2.4: 2001

* `Ubuntu releases
  <https://en.wikipedia.org/wiki/List_of_Ubuntu_releases#Table_of_versions>`_:

  - 16.10: Yakkety Yak (not released yet, scheduled for 2016-10-20)
  - 16.04 LTS: Xenial Xerus, 2016-04-21
  - 15.10: Wily Werewolf, 2015-10-22
  - 15.04: Vivid, 2015-04
  - 14.10: Utopic, 2014-10
  - 14.04 LTS: Trusty, 2014-04
  - 12.04 LTS: Precise, 2012-04

* `Fedora releases
  <https://en.wikipedia.org/wiki/Fedora_%28operating_system%29#Releases>`_:

  * Fedora 24: 2016-06-21
  * Fedora 23: 2015-11-03
  * Fedora 22: 2015-05-26
  * Fedora 21: 2014-12
  * Fedora 20: 2013-12, Heisenbug
  * Fedora 19: 2013-07, Schrödinger's Cat

* `Debian releases <https://www.debian.org/releases/>`_:

  * Debian 9 "Stretch": June 17th, 2017
  * Debian 8 "Jessie": April 26th, 2015

.. _freebsd-list:

`FreeBSD releases <https://en.wikipedia.org/wiki/FreeBSD#Version_history>`_,
and `Unsupported FreeBSD Releases
<https://www.freebsd.org/security/unsupported.html>`_:

============  =======  ===========
FreeBSD       Release  End of life
============  =======  ===========
FreeBSD 11.0  2016-10  2021-09-30
FreeBSD 10.0  2014-01  2018-10-31
FreeBSD 9.0   2012-01  2016-12
FreeBSD 8.1   2010-07  2012-07
FreeBSD 7.0   2008-02  2009-04
FreeBSD 6.2   2007-01  2008-05
============  =======  ===========

.. _windows-list:

`Microsoft Windows versions
<https://en.wikipedia.org/wiki/List_of_Microsoft_Windows_versions>`_
(`version numbers <https://msdn.microsoft.com/en-us/library/windows/desktop/ms724832(v=vs.85).aspx>`_):

===========================  =======  =======  =========================  ================
Windows                      Version  Release  End of mainstream support  Extended support
===========================  =======  =======  =========================  ================
Windows 10                      10.0  2015-07  2020-10                    2025-10
Windows 8.1                      6.3  2013-10  2018-01                    2023-01
Windows 8                        6.2  2012-10  2016-01                    2016-01
Windows 7                        6.1  2009-10  2015-01                    2020-01
Windows Vista                    6.0  2007-01  2012-04                    2017-04
Windows XP Professional x64      5.2  2005-04  2009-04                    2014-04
Windows XP                       5.1  2001-10  2009-04                    2014-04
===========================  =======  =======  =========================  ================

.. note::

   For applications that have been manifested for Windows 8.1 or Windows 10.
   Applications not manifested for Windows 8.1 or Windows 10 will return the
   Windows 8 OS version value (6.2). To manifest your applications for Windows
   8.1 or Windows 10, refer to Targeting your application for Windows.

Linux kernel:

* `Active kernel releases
  <https://www.kernel.org/category/releases.html>`_

============  ===========  =============
Linux kernel  Released     Projected EOL
============  ===========  =============
4.14          2017-11-12   2020-01
4.9           2016-12-11   2019-01
4.4           2016-01-10   2022-02
4.1           2015-06-21   2018-05
3.16          2014-08-03   2020-04
3.2           2012-01-04   2018-05
2.6           2003-12-17   2011-08
============  ===========  =============


Programming advices
===================

* Coding style: 80 columns, PEP 7 for C, PEP 8 for Python
* Avoid variable globals
* Signal handlers: only use signal-safe functions


Timezones
=========

* Debian issue: `tzdata: Argentina just decided not to move to DST this Sunday :-\
  <https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=551195>`_
* Python issue: `datetime: support leap seconds
  <https://bugs.python.org/issue23574>`_


rsync
=====

Local copy with progress bar and handle sparse files::

    rsync -Sav --progress /mnt/vm/images/ /var/lib/libvirt/images/

Thunderbird
===========

`Checking for new messages in other folders - Thunderbird
<http://kb.mozillazine.org/How_do_I_check_for_new_messages_in_other_folders>`_.

Set ``mail.server.default.check_all_folders_for_new=true`` in advanced settings
(Edit > Preference > Advanced > General tab > Config editor).


Gnome-Terminal
==============

Configure Gnome-Terminal to select a full URL double-click::

    dconf write /org/gnome/terminal/legacy/profiles:/:${Profile_ID}/word-char-exceptions '@ms "-,.;/?%&#_=+@~·:"'

Replace ``${Profile_ID}`` with the profile identifier. To get it::

    $ gsettings get org.gnome.Terminal.ProfilesList list
    ['b1dcc9dd-5262-4d8d-a863-c897e6d979b9']

Example::

    dconf write /org/gnome/terminal/legacy/profiles:/:b1dcc9dd-5262-4d8d-a863-c897e6d979b9/word-char-exceptions '@ms "-,.;/?%&#_=+@~·:"'

It looks like you don't have to restart Gnome-Terminal.

http://fedora.12.x6.nabble.com/gnome-terminal-amp-select-by-word-characters-td5043736.html

* https://bugzilla.redhat.com/show_bug.cgi?id=1165244
* https://bugzilla.redhat.com/show_bug.cgi?id=1227222
* https://bugzilla.gnome.org/show_bug.cgi?id=727743
* https://bugzilla.gnome.org/show_bug.cgi?id=730632#c33


Android
=======

Samsung S2, delete logs on internal storage:

* dial ``*#9900#``
* click on: "Delete dumpstate/logcat"

Free space on the 16 GB SD card:

* install CCleaner
* Free space using CCleaner


IRC
===

List operators of channel::

    /msg ChanServ access #python-fr list

Give operator permission to someone::

    /msg ChanServ flags #python-fr skyice +Aeiortv


SSH keygen
==========

Create an SSH key::

    ssh-keygen -t ed25519 -o -a 100 -C "haypo2017" -f ssh_key

* ``-t``: key type, http://ed25519.cr.yp.to/
* ``-a 100``: use 100 rounds of the key derivation function for the passphrase,
  increase resistance to brute-force password cracking
* ``-C``: comment
* ``-f``: filename
* ``-o``: save private keys using the new OpenSSH format, increased resistance
  to brute-force password cracking (in fact, ``-t ed25519`` already enables
  this option)

Issues with ed25519:

* Launchpad doesn't support ed25519: Launchpad is implemented on top of Twisted
  which doesn't support ed25519 yet.
  https://bugs.launchpad.net/launchpad/+bug/1282220
* gnome-keyrign doesn't support the new SSH key format used by ed25519 by
  default:
  https://bugzilla.gnome.org/show_bug.cgi?id=723274
  https://bugzilla.gnome.org/show_bug.cgi?id=641082

Links:

* https://stribika.github.io/2015/01/04/secure-secure-shell.html
* https://wiki.archlinux.org/index.php/SSH_keys

SSH agent:

* Modify /etc/pam.d/* to lines containing "pam_gnome_keyring.so"
* Make sure that login still works after the change!!!

Gnome and SSH passphrase::

    sudo dnf install -y openssh-askpass

Replace gnome-keyring with ssh-agent to support elliptic curves:

* https://ask.fedoraproject.org/en/question/92448/how-do-i-get-proper-ssh-agent-functionality-in-gnome/

Fedora process::

    /usr/bin/gnome-keyring-daemon --daemonize --login

Disable gnome-keyring::

    mkdir -p ~/.config/autostart/
    cp /etc/xdg/autostart/gnome-keyring-ssh.desktop ~/.config/autostart/
    echo "X-GNOME-Autostart-enabled=false" >>~/.config/autostart/gnome-keyring-ssh.desktop

See also https://wiki.archlinux.org/index.php/GNOME/Keyring#Disable_keyring_daemon_components

Enable pam_ssh in PAM config:

* https://wiki.archlinux.org/index.php/SSH_keys
* https://ask.fedoraproject.org/en/question/92448/how-do-i-get-proper-ssh-agent-functionality-in-gnome/


(FR) Transport aérien
=====================

* March 2014: https://fr.wikipedia.org/wiki/Vol_370_Malaysia_Airlines#Hypoth.C3.A8se_d.27un_incident_technique
* April 2016: Batteries lithium-ion interdites dans le transport de fret
  aérien.


Gnome
=====

My CSS theme for window colored borders: https://github.com/vstinner/misc/blob/master/conf/gtk.css

https://wiki.gnome.org/Projects/GnomeShell/CheatSheet

gsettings set org.gnome.desktop.wm.preferences focus-new-windows 'strict'


Yubikey
=======

* Fedora: dnf install -y u2f-hidraw-policy
  See https://gist.github.com/fntlnz/a4513162960e1e9fdb99
* Firefox: builtin since Firefox 57, see https://www.yubico.com/2017/11/how-to-navigate-fido-u2f-in-firefox-quantum/
  For older Firefox, use https://addons.mozilla.org/fr/firefox/addon/u2f-support-add-on/
  (proect: https://github.com/prefiks/u2f4moz)
* GitHub: https://github.com/settings/two_factor_authentication/configure click on [Register new device]
* Firefox plugin doesn't work on Google nor Bitbucket


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
  * Add a new user: username haypo
  * Exit: Manual config? No
  * Reboot

* (After reboot)
* Log as root
* type "pkg sudo" and install it
* run "visudo" and uncomment "%whell ALL.." without password
* add haypo user to the wheel group: pw group mod wheel -m haypo
* Relog as haypo
* sudo pkg install bash git
* chsh: write /usr/local/bin/bash (check before with "which bash")
* Delog, log again as haypo

Change the keyboard layout: run ``kbdmap``.


tmux
====

* tmux attach
* tmux ls
* CTRL+b ...

  - ``d``: detach
  - ``c``: new window
  - ``n`` / ``p``: next/previous window
  - ``:``: open the command line ("prompt")
  - ``,``: name the window
  - ``w``: window list
  - ``&``: kill the window

* Command line or "prompt" (opened by CTRL+b :):

  - list-sessions

* `tmux shortcuts & cheatsheet <https://gist.github.com/MohamedAlaa/2961058>`_


Debug Python
============

* Add printf(...) of fprintf(stderr, ...)
* Comment, remove code, add #if 0 ... #endif
* Run git bisect
* Use my new script to bisect test *methods*
* gdb
* pdb, pudb

NFS
===

Server side
-----------

* ``/etc/exports``: list of shared directories
* ``sudo exportfs -af``: reload NFS configuration (like ``/etc/exports``)

Client side
------------

* Mount: ``sudo mount -t nfs -o soft smithers:/server/shared/directory /local/mount/point``.
  The ``soft`` option allows NFS to make syscalls failing if the server is no
  more reachable.
* Unmount: ``sudo umount -f /local/mount/point``, ``-f`` allows to unmount
  even if the server is unreachable.


Release a Python software
=========================

* pip install check-manifest
* pip install prospector[pyroma]; prospector
* zest.releaser

macOS
=====

Firefox malware: "Websecure WTC", system load near 10, CPU usage higher than
99%. Remove manually in Firefox extensions.

Anti-malware: don't trust the internet, full of crap. Search in AppStore.

Untested yet: free Bitdefender.

Rounding
========

Wikipedia: https://en.wikipedia.org/wiki/Rounding

Rounding modes for floating point numbers:

* ROUND_FLOOR: Round towards minus infinity (-inf).

  * C: ``floor()``
  * Python: ``math.floor(float)``
  * Python: ``math.floor(-0.1) == -1``
  * Python: ``math.floor(0.9) == 0``
  * For example, used to read a clock.

* ROUND_CEILING: Round towards infinity (+inf).

  * Python: ``math.ceil(float)``
  * Python: ``math.ceil(0.1) == 1``
  * Python: ``math.ceil(-0.1) == 0``

* ROUND_HALF_EVEN: Round to nearest with ties going to nearest even integer.

  * For example, used to round from a Python float.
  * Python: ``round(float)``
  * Python: ``round(0.5) == 0``
  * Python: ``round(1.5) == 2``
  * Python: ``round(2.5) == 2``

* ROUND_UP: Round away from zero.

  * For example, used for timeout. ROUND_CEILING rounds -1e-9 to 0 milliseconds
    which causes bpo-31786 issue. ROUND_UP rounds -1e-9 to -1 millisecond which
    keeps the timeout sign as expected. select.poll(timeout) must block for
    negative values.

* ROUND_DOWN: Round towards zero.

  * C: (int)double, ex: ``(int)0.9 == 0``
  * Python: ``int(float)``
  * Python: ``int(0.9) == 0``
  * Python: ``int(-0.9) == 0``
  * Python: ``float.__trunc__()``

Other rounding modes (ex: Python decimal module):

* ROUND_HALF_DOWN: Round to nearest with ties going towards zero.
* ROUND_HALF_UP: Round to nearest with ties going away from zero.
* ROUND_05UP: Round away from zero if last digit after rounding towards zero
  would have been 0 or 5; otherwise round towards zero.

IEEE 754 defines 4 modes:

* ROUND_HALF_EVEN: **default mode**
* ROUND_FLOOR
* ROUND_CEILING
* ROUND_DOWN

See also: https://vstinner.github.io/pytime.html


Process wide vs multithreading
==============================

Multithreading is hard because many functions of system C library (libc):

* modify a state for the whole process: change process wide
* is not reentrant
* rely on a global state
* is not "async signal safe"

Examples of process-wide states:

* *Current working directory* aka **cwd**

  * Modified by ``chdir()``
  * Most "legacy" filesystem functions taking a filename rely on the "current
    working directory" (cwd), especially using relative path. Exampes:
    ``open()`` or ``chmod()``.
  * The new Linux "at" functions don't rely on the current working directory.
    Examples: openat() or chmodat().

* Locales

  * Modified by ``setlocale()``
  * For example, used by ``strftime()`` and ``localeconv()``.
  * Functions using "wide character strings" (wcs) avoid some issues.
    Example: ``wcsftime()``.
  * Some libraries don't rely on a global locale but expect a locale argument

* Unix signals

  * Signal handlers are registered by signal() and sigaction()
  * ``raise()`` or ``kill()`` to send a signal to a process
  * Per thread API: ``pthread_kill()`` (send a signal to a thread),
    ``pthread_sigmask()`` (block signals)

Others:

* File descriptors: not really an issue in practice if a FD is only used
  in a single thread.
* Heap memory, malloc()/free(): modern malloc() implementations scales on
  threads/CPUs. Not an issue if a memory block is only used in a single thread.
* User and groups

See also `Ghosts of Unix Past: a historical search for design patterns
<https://lwn.net/Articles/411845/>`_ by Neil Brown (October, 2010).


Linux: follow process execution
===============================

* `execsnoop <http://www.brendangregg.com/blog/2014-07-28/execsnoop-for-linux.html>`_
* `linux process monitoring <http://bewareofgeek.livejournal.com/2945.html>`_:
  NETLINK_CONNECTOR with CN_IDX_PROC and CN_VAL_PROC commands


wget mirror
===========

Download a "Index of" Apache listing and subdirectories, but not parents.

wget --mirror --no-parent -e robots=off URL

robots=off is needed to downloda OpenStack CI logs, since the robots.txt
disallow everything.

dd
==

Write a raw image to a USB key::

    lsblk # check if the USB key is connected
    sudo dd if=bios.img of=/dev/disk/by-id/usb-LEXAR_JUMPDRIVE_0A4F1007191812160305-0\:0 status=progress oflag=direct


ssh-agent
=========

List keys of ssh-agent::

    ssh-add -l

Add a key::

    ssh-add ~/.ssh/id_rsa

Remove all keys::

    ssh-add -D


stdin, stdout, stderr buffering
===============================

Unbuffered standard streams with the stdbuf tool::

    stdbuf -i0 -o0 -e0 producer | consumer

Line buffering::

    stdbuf -oL -eL command

See also unbuffer.

Copy for backup using rsnyc
===========================

Commands::

    $ sudo mount -o uid=haypo,gid=haypo,utf8 /dev/disk/by-label/DataSeagate /mnt/usb/
    $ rsync --archive --verbose --progress -r /btrfs/data/videos/  /mnt/usb/videos/


virt-manager: virtual network
=============================

Enable Router Advertissement on your phyiscal devices.

* Create file ``/etc/sysctl.d/60-victor-network.conf``::

    net.ipv6.conf.enp0s31f6.accept_ra = 2
    net.ipv6.conf.wlp4s0.accept_ra = 2

  where ``enp0s31f6`` and ``wlp4s0`` are my physical NICs.

* Run::

    sudo systemctl restart systemd-sysctl

Virt-manager, create a network:

* Right click on a domain, Detail: Network, Add a network
* IPv4 Network: 192.168.100.0/24 ; enable DHCP
* IPv6 Network: fd00:e81d:a6d7:5ab8::/64 ; enable DHCPv6
* Give access to any physical NIC

Install FreeBSD VM
==================

* https://www.freebsd.org/where.html : Download amd64/qcow2 virtual machine image,
* Uncompress the image: unxz file.qcow2.xz
* Move the image to /var/lib/libvirt/images/
* Create a FreeBSD VM using this disk image
* kbdcontrol -l fr.iso
* Log as root
* pkg install sudo bash screen
* adduser: add user, add it to the wheel group
* visudo: allow sudo for the whell group
* Unlog, log again as the new user
* chsh -s /usr/local/bin/bash
* Unlog, log again (to get bash)
* Enable the SSH server:

 * Add sshd_enable="YES" to /etc/rc.conf
 * service sshd start
 * https://www.freebsd.org/doc/handbook/openssh.html


Status pages
============

* Python : https://status.python.org/
* GitHub : https://status.github.com/ and https://twitter.com/githubstatus
* Travis CI : https://www.traviscistatus.com/ and https://twitter.com/traviscistatus

KDE Connect on Fedora
=====================

Commands::

    sudo dnf install kde-connect-nautilus
    sudo firewall-cmd --zone=public --permanent --add-port=1714-1764/tcp
    sudo firewall-cmd --zone=public --permanent --add-port=1714-1764/udp
    sudo systemctl restart firewalld.service

See also https://community.kde.org/KDEConnect

docker
======

sudo docker pull ubuntu:trusty
sudo docker run -ti ubuntu:trusty /bin/bash
root@xxx# exit
sudo docker commit xxx pet
sudo docker run -ti pet /bin/bash
sudo docker container ps
sudo docker container ps -a
