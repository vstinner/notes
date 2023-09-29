++++++++++++++
Unsorted Notes
++++++++++++++

.. image:: great_flamingo.jpg
   :alt: Great Flamingo
   :align: right
   :target: http://www.flickr.com/photos/haypo/11915292626/

GitHub
======

* https://github.com/pulls/review-requested

URLs:

* Add ``?w=1`` in a pull request to ignore whitespace changes
* Add ``.patch`` to a pull request to get the change as an unified diff
* In a message, ``<details> ... </details>`` creates a drop-down

Markdown:

* ``<details>`` can be used for long fold/unfold list, traceback, etc.

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

    $ git tag --contains 94a3b83f9f1fd52a78b9d49b32ddfae40182f852
    12.0.0.0b1
    12.0.0a0
    2014.2
    2014.2.1
    ...


Remote branches
---------------

* List remote branches: ``git branch -r``
* Create a new branch ``fix_1369426_icehouse`` tracking the remote branch
  ``origin/stable/icehouse``::

    git branch --track fix_1369426_icehouse origin/stable/icehouse

* (Track and) Pull a remote branch::

    git branch --track NAME_REMOTE_BRANCH
    git fetch --all   # or: git pull --all


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
* ``<<<"HELLO"`` syntax, known as "here-string", creates a temporary file which
  contains the string ``HELLO`` and uses this file as the child process
  ``stdin`` (fd 0).
* ``"$(...)"`` syntax allows to pass the output of a command to a program with newline characters::

    python3 -c "$(echo -e "for i in range(3):\n  print(i)")"

Example::

    haypo@selma$ echo $'a\rb'|hexdump -C
    00000000  61 0d 62 0a                                       |a.b.|
    00000004

* sh is supposed to be the minimalist shell (faster, but less feature)
* bash has more feature and is quite common, but not available by default
  on FreeBSD for example.
* dash is a minimalist shell used as 'sh' on Debian

Test:

* [ is a program: /usr/bin/[ on Linux
* man test
* man [ # sometimes display bash manual page
* [[ ... ]] is a bash built-in, so specific to bash

Replace ``name.py`` string with ``name``, remove ``.py`` suffix::

    script="name.py"
    # display "name"
    echo ${script:0:-3}

Misc:

* https://pypi.org/project/bashate/

Friends
=======

* http://blog.sileht.net/
* http://www.florentflament.com/
* http://yeknan.free.fr/dc2/

Fun:

* http://tumourrasmoinsbete.blogspot.fr/
* http://www.commitlogsfromlastnight.com/


Google
======

What Google knowns on you:

* https://myactivity.google.com/
* https://myaccount.google.com/
* https://maps.google.fr/locationhistory/
* https://takeout.google.com/


.. _operating-systems:

Operating systems
=================

.. _macos-list:

`macOS (Mac OS X) versions
<https://en.wikipedia.org/wiki/macOS#Release_history>`_:

==============  ============== ==============  ============
macOS           Name           Darwin Version  Release Year
==============  ============== ==============  ============
macOS 14        Sonoma         23.x            2023 (Sep)
macOS 13        Ventura        22.x            2022 (Oct)
macOS 12        Monterey       21.x            2021 (Oct)
macOS 11        Big Sur        20.x            2020 (Nov)
macOS 10.15     Catalina       19.x            2019 (Oct)
macOS 10.14     Mojave         18.x            2018 (Sep)
macOS 10.13     High Sierra    17.x            2017 (Jun)
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

Use ``sw_vers`` in the command line to get macOS version.

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


Gnome-Terminal
==============

Configure Gnome-Terminal to select a full URL double-click::

    dconf write /org/gnome/terminal/legacy/profiles:/:${Profile_ID}/word-char-exceptions '@ms "-,.;/?%&#_=+@~·:"'

Replace ``${Profile_ID}`` with the profile identifier. To get it::

    $ gsettings get org.gnome.Terminal.ProfilesList list
    ['b1dcc9dd-5262-4d8d-a863-c897e6d979b9']

Example::

    dconf write /org/gnome/terminal/legacy/profiles:/:b1dcc9dd-5262-4d8d-a863-c897e6d979b9/word-char-exceptions '@ms "-,.;/?%&#_=+@~·:"'

To see notifications on irssi, use XTerm color theme, rather than the default
"Tango" theme: XTerm theme has a better contrast.


Android
=======

Avoid music applications (Spotify, radio) to stop when idle (phone locked):

* Parameters > Network > Save data > select application:
  allow your music applications
* Parameters > Batterie > Applications:
  allow your music applications


IRC
===

Give operator and owner permission to *mdk*::

    /msg chanserv FLAGS #python-fr mdk +AFRefiorstv

Kick a spammer with a link to AFPy charter::

    /msg ChanServ AKICK #python-fr ADD spammer_nickname !T 1h https://www.afpy.org/docs/charte

List operators of channel::

    /msg ChanServ access #python-fr list

#python-dev flags to prevent people who are not logged in to an account from
talking::

   /mode #python-dev -q $~a


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


tmux
====

* tmux attach
* tmux ls
* CTRL+b ...

  - ``[``: navigation (scroll), 'q' to quit navigation mode
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
  * This is the default rounding mode used in IEEE 754 floating-point
    operations.

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

Links:

* https://vstinner.github.io/pytime.html
* "double-rounding" https://bugs.python.org/issue24567
* https://bugs.python.org/issue32956
* double to float rounding on ppc64le: https://gcc.gnu.org/bugzilla/show_bug.cgi?id=88892


Linux: follow process execution
===============================

* `execsnoop <http://www.brendangregg.com/blog/2014-07-28/execsnoop-for-linux.html>`_
* `linux process monitoring <http://bewareofgeek.livejournal.com/2945.html>`_:
  NETLINK_CONNECTOR with CN_IDX_PROC and CN_VAL_PROC commands
* `exec-notify.c  <https://gist.github.com/L-P/9487407>`_:
  PROC_EVENT_EXEC reading /proc/pid/cmdline

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


Status pages
============

* Python : https://status.python.org/
* GitHub : https://www.githubstatus.com/ and https://twitter.com/githubstatus
* Travis CI : https://www.traviscistatus.com/ and https://twitter.com/traviscistatus

KDE Connect on Fedora
=====================

Commands::

    sudo dnf install kde-connect-nautilus
    sudo firewall-cmd --zone=public --permanent --add-port=1714-1764/tcp
    sudo firewall-cmd --zone=public --permanent --add-port=1714-1764/udp
    sudo systemctl restart firewalld.service

See also https://community.kde.org/KDEConnect

SELinux
=======

Display SELinux alerts in Gnome: ``sealert``.

Dummy command to restore SELinux labels on the whole operating system::

    restorecon -Rv /

``/etc/selinux/config`` config file::

   SELINUX=enforcing
   SELINUXTYPE=targeted

Check current SELinux config::

   $ getenforce
   Enforcing

posix_spawn
===========

Python issues:

* `expose posix_spawn(p)
  <https://bugs.python.org/issue20104>`_
* `Support POSIX_SPAWN_USEVFORK flag in posix_spawn
  <https://bugs.python.org/issue34663>`_
* `subprocess uses os.posix_spawn in some cases
  <https://bugs.python.org/issue35537>`_

vfork:

* https://ewontfix.com/7/

Performance:

* https://github.com/rtomayko/posix-spawn


Valgrind
========

Search for memory leak: malloc() not followed by free(), limit the call stack
to 20 frames::

    PYTHONMALLOC=malloc valgrind --leak-check=full --show-leak-kinds=all --log-file=valgrind.log --num-callers=20 ./python script.py

`Valgrind with gdb server
<http://valgrind.org/docs/manual/manual-core-adv.html>`_ to inspect a bug in gdb::

    # First terminal
    valgrind --vgdb=yes --vgdb-error=0 program [arg1 arg2 ...]

    # Second terminal
    gdb
    # then type in gdb:
    # (gdb) target remote | vgdb

Generate a suppression for a false alarm::

    --gen-suppressions=yes

Python issues related to Valgrind:

* https://bugs.python.org/issue38118
* https://bugs.python.org/issue37329


Floating point number
=====================

Binary IEEE 754:

* http://fabiensanglard.net/floating_point_visually_explained/
* Python 3.9: math.ulp(), math.nextafter()
* http://0.30000000000000004.com/

Other:

* `GMP <https://gmplib.org/>`_: free library for arbitrary precision
  arithmetic, operating on signed integers, rational numbers, and
  floating-point numbers.
* `MPFR <https://www.mpfr.org/>`_: multiple-precision floating-point
  computations with correct rounding. MPFR is based on the GMP
  multiple-precision library.
* `MPFI <https://gforge.inria.fr/projects/mpfi/>`_: multiple precision
  **interval** arithmetic library based on MPFR


Mplayer
=======

Increase maxiumum volume::

    mplayer -softvol -softvol-max 300 video.avi


Virtualization: run an AArch64 VM on x86-64
===========================================

Before starting virt-manager, install (``edk2-aarch64`` is for UEFI)::

    sudo dnf install qemu-system-aarch64 edk2-aarch64

In virt-manager, pick "arch: AArch64" in the first dialog of the wizard.

* https://fedoraproject.org/wiki/Architectures/AArch64/Install_with_QEMU


Coredump Linux
==============

Default configuration::

    $ cat /proc/sys/kernel/core_pattern
    |/usr/lib/systemd/systemd-coredump %P %u %g %s %t %c %h

Create coredump file in the current directory::

    sudo bash -c 'echo "%e.%p.core" > /proc/sys/kernel/core_pattern'

Create coredump filename like ``python-123.core``.

Maximum core dump size::

    $ ulimit -c
    unlimited

Test::

    $ ./python -c 'import ctypes; ctypes.string_at(0)'
    Segmentation fault (core dumped)
    $ ls *.core
    python.347656.core

See also ``man core``.


Contributions to open source
============================

GCC bug reports:

* https://gcc.gnu.org/bugzilla/show_bug.cgi?id=93384
* https://gcc.gnu.org/bugzilla/show_bug.cgi?id=88892
* https://gcc.gnu.org/bugzilla/show_bug.cgi?id=47271


Firefox
=======

* `In Firefox, what are smart keywords and how do I use them? <https://kb.iu.edu/d/arjb>`_
* URL bar:

  * ``* pulls`` searchs for "pulls" in bookmarks
  * ``^ pulls`` searchs for "pulls" in history
  * ``% pulls`` searchs for "pulls" in tabs

``about:config``:

* image.animation = once (default = "normal")
* mousewheel.with_alt.action = 1:

  * https://fedoraproject.org/wiki/Common_F32_bugs#Trying_to_scroll_with_mouse_wheel_in_inactive_Firefox_window_results_in_back.2Fforward_instead
  * https://bugzilla.redhat.com/bugzilla/show_bug.cgi?id=1650051
  * https://gitlab.gnome.org/GNOME/gtk/issues/2112

* ``privacy.webrtc.legacyGlobalIndicator`` to set **false** to hide the "Share
  indicator" (orange microphone/webcam indicator) window during video calls


Enter namespace filesystem of a Flatpak application or container
================================================================

If a Flatpak application is the pid 76688, inspect the process with:

* /proc/76688/root/ : Filesystem of the process.
* /proc/76688/mountinfo : Mount informations
* /proc/76688/ns/mnt : points to "mnt:[4026533594]"

For example, in a Flatpak application, the first line of mountinfo is something
like "(...) /newroot / rw,nosuid,nodev,relatime - tmpfs tmpfs (...)" which
means that the whole operating system is in memory, not on disk. Only following
mounts can map to directories on the machine disk.

See also the ``nsenter`` command, and ``ip netns help`` for network namespaces.

Debian
======

* List files contained in a package: ``dpkg --listfiles python3.9-dev``.
* Search which package contains a file: ``dpkg -S /path/to/file``.

Gmail filters
=============

* `Google Support: Gmail filters
  <https://support.google.com/mail/answer/7190?hl=en>`_
* `GitHub notifications
  <https://docs.github.com/en/rest/reference/activity#notifications>`_
* `Manage GitHub notification messages in Gmail with Google Apps Scripts
  <https://lyzidiamond.com/posts/github-notifications-google-script>`_

Dev Cython
==========

Run a single test of the Cython test suite::

    python runtests.py '.*test_unicode.*' -vv

Compile ``file.pyx`` to ``file.c``::

    python -m cython file.pyx

or::

    cython file.pyx

Compile ``file.pyx`` to ``file.c`` and builds a dynamic library (C extension)::

    cythonize -i file.pyx

Documentation: `Source Files and Compilation <https://cython.readthedocs.io/en/stable/src/userguide/source_files_and_compilation.html>`_


Video for Linux (V4L): control your webcam
==========================================

* GUI: ``gtk-v4l``
* CLI: ``v4l2-ctl --list-devices``


Copyright
=========

* https://github.com/pythoncapi/pythoncapi_compat/commit/14c4ade30c05153e9aa0ccd85bb7743ee0fdb5cb
* https://github.com/MatthieuDartiailh/bytecode/pull/91
* https://www.linuxfoundation.org/blog/copyright-notices-in-open-source-software-projects/
* https://hynek.me/til/copyright-years/


Licenses
========

* issue: `pythoncapi_compat.h is MIT licensed
  <https://github.com/MagicStack/immutables/pull/64>`_
* `Clarify the license of the included pythoncapi_compat.h header
  <https://github.com/MagicStack/immutables/commit/67c5edfb8284e39ab6a0be9a4644ede306c6e9bd>`_
* Strict license agreement: `zodbpickle
  <https://github.com/zopefoundation/zodbpickle/pull/64>`_


LVM
===

Hierarchy:

* Disks and disk partitions (primary/secondary)

  * ``lsblk``
  * ``parted /dev/vda``
  * (parted) Extend the second partition: ``resizepart 2 100%``

* LVM Physical Volume (PV)

  * ``pvs``
  * ``pvscan``
  * Extend a PV: ``pvresize /dev/vda2``

* LVM Volume Group (VG)

  * ``vgdisplay``
  * ``vgs``
  * ``vgscan``

* LVM Logical Volume (LV)

  * ``lvscan``
  * Add 6 GB to ``/root``: ``lvextend -L +6G /dev/vg_root_python-builder-rhel7.osci.io/root``
  * Add all free space to ``/home``: ``lvextend -l +100%FREE /dev/vg_root_python-builder-rhel7.osci.io/home``

* Filesystem (ext4, XFS, btrfs, etc.)

  * ``df -h``
  * Resize ``/root`` to its LV: ``resize2fs /dev/mapper/vg_root_python--builder--rhel7.osci.io-root``
  * Resize ``/home`` to its LV: ``resize2fs /dev/mapper/vg_root_python--builder--rhel7.osci.io-home``


Blockchain
==========

* https://web3isgoinggreat.com/
* https://defiwatch.net/

C++ language
============

``__cplusplus`` macro:

* C++98: 199711
* C++11: 201103
* C++14: 201402
* C++17: 201500


Hardware bugs
=============

* CPU bugs: `Cores that don’t count
  <https://sigops.org/s/conferences/hotos/2021/papers/hotos21-s01-hochschild.pdf>`_:
  "silent data corruption" (SDC).
  See also `Silent Data Corruption
  <https://support.google.com/cloud/answer/10759085?hl=en>`_.
* `Skylake bug: a detective story
  <https://tech.ahrefs.com/skylake-bug-a-detective-story-ab1ad2beddcd>`_ (2017)
  by Joris Giovannangeli.
  OCaml: bug in CPU microcode of Intel Kaby Lake and Skylake.
* `Machine-check exception (MCE)
  <https://en.wikipedia.org/wiki/Machine-check_exception>`_

Slack
=====

* https://allthings.how/how-to-turn-off-animated-emojis-and-gifs-in-slack/

Programming Principles
======================

* `Chesterton’s fence
  <https://en.wikipedia.org/wiki/Wikipedia:Chesterton%27s_fence>`_:
  "reforms should not be made until the reasoning behind the existing state of
  affairs is understood".

* `Hyrum's Law
  <https://www.hyrumslaw.com/>`_:
  "With a sufficient number of users of an API, it does not matter what you
  promise in the contract: all observable behaviors of your system will be
  depended on by somebody".

  * https://xkcd.com/1172/

* `Wirth's law
  <https://en.wikipedia.org/wiki/Wirth%27s_law>`_:
  "Software is getting slower more rapidly than hardware is becoming faster".

* `Law of triviality
  <https://en.wikipedia.org/wiki/Law_of_triviality>`_ aka
  "Bikeshedding":
  "People within an organization commonly or typically give disproportionate
  weight to trivial issues".

* `Heisenbug
  <https://en.m.wikipedia.org/wiki/Heisenbug>`_:
  "software bug that seems to disappear or alter its behavior when one attempts
  to study it".

* `Missing stair
  <https://en.wikipedia.org/wiki/Missing_stair>`_

GNOME Settings
==============

Resize a window with Super key ("Windows") + Right Click and then move the
mouse::

    gsettings set org.gnome.desktop.wm.preferences resize-with-right-button true

fwupdmgr
========

Update::

    sudo fwupdmgr update


Sanitizer
=========

Fedora::

    dnf install libasan

Tools:

* ASAN: Address Sanitizer
* LSAN: Leak Sanitizer (integrated in Address Sanitizer)
* MSAN: Memory Sanitizer
* TSAN: Thread Sanitizer
* UBSAN: Undefined Behavior Sanitizer

Environment variables:

* ``ASAN_OPTIONS`` (ASAN)
* ``LSAN_OPTIONS`` (LSAN)
* ``MSAN_OPTIONS`` (MSAN)
* ``TSAN_OPTIONS`` (TSAN)
* ``UBSAN_OPTIONS`` (UBSAN)

Documentation:

* LLVM

  * https://clang.llvm.org/docs/AddressSanitizer.html
  * https://clang.llvm.org/docs/LeakSanitizer.html
  * https://clang.llvm.org/docs/MemorySanitizer.html
  * https://clang.llvm.org/docs/ThreadSanitizer.html
  * https://clang.llvm.org/docs/UndefinedBehaviorSanitizer.html

* Google

  * https://github.com/google/sanitizers/wiki/SanitizerCommonFlags
  * https://github.com/google/sanitizers/wiki/AddressSanitizer

Python configure options:

* ``--with-address-sanitizer`` (ASAN)
* ``--with-memory-sanitizer`` (MSAN)
* ``--with-undefined-behavior-sanitizer`` (UBSAN)

podman to create Ubuntu image
=============================

https://community.endlessos.com/t/running-ubuntu-with-podman/10506

Create Ubuntu 23.04 container::

    podman image pull ubuntu:23.04
    podman image list --all
    podman run --name ubuntu-dev --hostname ubuntu-dev --interactive --tty ubuntu:23.04

In the container::

    # create vstinner user
    useradd -d /home/vstinner -s /bin/bash vstinner
    mkdir /home/vstinner/
    chmod -R 700 /home/vstinner
    chown -R vstinner:users /home/vstinner
    exit

Start the container::

    podman run --name ubuntu-dev --interactive --tty ubuntu:23.04

user shell::

     podman exec --interactive --tty --user vstinner --workdir /home/vstinner ubuntu-dev /bin/bash

root shell::

    podman exec --interactive --tty ubuntu-dev /bin/bash

Stop container::

    podman stop ubuntu-dev

Remove container::

    podman rm ubuntu-dev

Build Python::

    # root
    apt update
    apt install sudo tmux git make gcc -y
    apt install -y libssl-dev libffi-dev ncurses-dev libbz2-dev libreadline-dev lzma-dev uuid-dev libgdbm-dev
    apt install clang

    # user
    cd
    git clone https://github.com/python/cpython --depth 1
    cd cpython
    ./cpython/configure --with-address-sanitizer --without-pymalloc --with-pydebug
    make -j14

GRUB
====

* https://fedoraproject.org/wiki/Changes/HiddenGrubMenu

Show GRUB menu at boot (timeout of 5 seconds)::

    sudo grub2-editenv - unset menu_auto_hide

GNOME Emoji
===========

* Press CTRL+. to open GNOME built-in Emoji Picker. It doesn't work in all
  apps.
* Press [Windows] key and type an emoji name to search for emoji characters.
* Install `Smile <https://smile.mijorus.it/>`_ from Software, it's a Flatpak
  application.
* Go to GNOME Parameters > Keyboard > Shortcuts > Customized shortcuts.
  Add a customized shortcut.

  * Name: Smile
  * Command: ``flatpak run it.mijorus.smile``
  * Shortcut: ALT+j
  * Well, for me "j" remains me "emoJi", but I'm using ALT+e to spawn
    a new terminal :-)

* See also https://emojipedia.org/

NAND Game
=========

Design your logic games to make an ALU and then a whole CPU!

https://nandgame.com/
