+++++++
systemd
+++++++

List services
=============

Find the name of the systemd unit for MariaDB or RabbitMQ server.

List all installed services, including disabled services, and search for "maria"::

    systemctl list-unit-files --type=service | grep maria

Alternative if you know the package name::

    $ rpm -ql mariadb-server|grep service
    /usr/lib/systemd/system/mariadb.service

List enabled services::

    systemctl list-units

Note: it looks like "list-units" doesn't show mariadb.service, probably because
it is disabled (not started at boot).


System logs: journald and journalctl
====================================

* Binary logs are written into ``/var/log/journal/``
* Show syslog from the most recent to the oldest logs: ``journalctl --reverse``
* Show all logs since the last boot: ``journalctl -b 0``
* List boots: ``journalctl --list-boots``
* ``tail -f /var/log/syslog``: ``journalctl -f``
* ``tail -f /var/log/syslog`` but only for apache: ``journalctl -u apache.service -f``
* Kernel logs of the current boot: ``journalctl -k`` (similar to ``dmesg`` but
  with better timestamp)
* Retain only journald logs of the past 30 days:
  ``journalctl --vacuum-time=30d``
* Filters:

  * ``journalctl _PID=7797`` show logs of process pid 7797
  * ``journalctl _COMM=chronyd -r`` shows latest logs of the program ``chronyd``

* Other fields:

  * ``_EXE``: program full path
  * ``_CMDLINE``: program command line with arguments
  * ``_UID``: user identifier
  * ``_GID``: group identifier
  * ``_BOOT_ID``: boot UUID
  * ``_MACHINE_ID``: machine UUID
  * ``_HOSTNAME``: hostname
  * ``SYSLOG_IDENTIFIER``

* See all journalctl fields: ``journalctl -o export``

Example of a single log entry (in ``export`` mode)::

    __CURSOR=s=c9faccefcf184d67b8a1a1a8c9441d83;i=9417;b=b6852be278a647e3b1f1047604d828c8;m=3e8ae848;t=5a093d6b361fa;x=2c3f533b3fc622ed
    __REALTIME_TIMESTAMP=1583931706270202
    __MONOTONIC_TIMESTAMP=1049290824
    _BOOT_ID=b6852be278a647e3b1f1047604d828c8
    PRIORITY=6
    SYSLOG_FACILITY=3
    _UID=1000
    _GID=1000
    _SELINUX_CONTEXT=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
    _AUDIT_SESSION=3
    _AUDIT_LOGINUID=1000
    _SYSTEMD_OWNER_UID=1000
    _SYSTEMD_UNIT=user@1000.service
    _SYSTEMD_SLICE=user-1000.slice
    _SYSTEMD_USER_SLICE=-.slice
    _MACHINE_ID=1a6df4a3ce76477790264e5d3a9fa609
    _HOSTNAME=apu
    _TRANSPORT=stdout
    SYSLOG_IDENTIFIER=gnome-shell
    _COMM=gnome-shell
    _EXE=/usr/bin/gnome-shell
    _CMDLINE=/usr/bin/gnome-shell
    _CAP_EFFECTIVE=800000
    _SYSTEMD_CGROUP=/user.slice/user-1000.slice/user@1000.service/gnome-shell-wayland.service
    _SYSTEMD_USER_UNIT=gnome-shell-wayland.service
    _PID=1702
    _SYSTEMD_INVOCATION_ID=5afe30294e9c49d6b27ff3011323619a
    _STREAM_ID=e46f4fd89cd3445fbac494d0814d34a5
    MESSAGE
    <80>^@^@^@^@^@^@^@libinput error: client bug: timer event13 debounce short: scheduled expiry is in the past (-5ms), your system is too slow

Advantages over scattered text log files:

* Timestamps seem to be more reliable, especially for kernel logs
* Ability to display logs in the reverse order
* Ability to filter logs by service, by user, by process pid, by boot, etc.
* ... in fact, I rarely use logs, so I don't have strong expectations for logs
  :-)


Advantages of systemd to run services
=====================================

* I like systemd global design to build "stateless" services, by isolating them
  from the system for example.
* Security: systemd gives access to high level security protections like
  running a service with its own private temporary directory ``/tmp`` (option
  ``PrivateTmp``). Options:

  * ``ProtectKernelModules=yes``
  * ``MemoryDenyWriteExecute=yes``
  * ``RestrictRealtime=yes``
  * ``PrivateNetwork=yes``
  * ``PrivateTmp=yes``
  * ``ProtectSystem=yes``
  * ``ProtectHome=yes``
  * Read also `Using systemd for more secure services in Fedora
    <https://lwn.net/Articles/709755/>`_

* systemd can even create a couple of temporary (user, group) to run a service
  and remove theme once the service stops. To be able to implement this
  feature, systemd has to cleanup all resources owner by the user. Running
  the service with a read-only filesystem except of a single writable directory
  helps to remove all files created by the service. Removing all IPC owned by
  a user is part of this cleanup (option ``RemoveIPC``).

* ``systemctl status service`` shows the last log lines.

* Thanks to cgroups, systemd is able to list all processes of a service in a
  secure manner. ``systemctl status service`` lists all process identfiers
  of the service (main pid, but also pids of child processes). Moreover, when
  systemd stops a service, the usage of a cgroups makes sure that all processes
  are killed. Bye bye the legacy and annoying "pid file" causing so many
  troubles.

* The simple ``.service`` file format makes it much easier to share these files
  between Linux distributions. Linux distributions can collaborate on more complex
  issues like handling properly NFS mounts: `Systemd programming, 30 months
  later <https://lwn.net/Articles/701549/>`_. Moreover, it's easier to enable
  security protections for all Linux distributions.

There is a similar trend to isolate desktop applications using sandboxes: see
`Flatpak <https://flatpak.org/>`_. For security, but also to reduce
dependencies to the system, and so run an old application on a newer system, or
the opposite. Embedding libraries in Flatpak "containers" comes with its own
set of issues, but that's a different topic ;-)

.. _coredumpctl:

coredumpctl
===========

See also :ref:`Fedora ABRT <abrt>`.

Configuration: https://www.freedesktop.org/software/systemd/man/coredump.conf.html

See also: https://wiki.archlinux.org/index.php/Core_dump

coredumpctl checks for coredump in ``/var/lib/systemd/coredump/`` directory::

    $ coredumpctl list
    TIME                            PID   UID   GID SIG COREFILE  EXE
    Wed 2020-03-11 13:46:38 CET    3350  1000  1000  11 present   /usr/bin/python3.7
    Wed 2020-03-11 13:48:28 CET    2211  1000  1000  11 present   /usr/bin/abrt-applet

    $ coredumpctl dump /usr/bin/abrt-applet > core
               PID: 2211 (abrt-applet)
    (...)
            Signal: 11 (SEGV)
         Timestamp: Wed 2020-03-11 13:48:27 CET (30min ago)
      Command Line: /usr/bin/abrt-applet --gapplication-service
    (...)
           Storage: /var/lib/systemd/coredump/core.abrt-applet.1000.b6852be278a647e3b1f1047604d828c8.2211.1583930907000000000000.lz4
           Message: Process 2211 (abrt-applet) of user 1000 dumped core.

                    Stack trace of thread 2211:
                    #0  0x00007f978e419fec problem_get_argv0 (libreport-gtk.so.0)
                    #1  0x00005632d09a4d83 notify_problem_list (abrt-applet)
                    #2  0x00005632d09a5291 show_problem_list_notification (abrt-applet)
    (...)

systemd trolls
==============

systemd features are not unique, it's totally doable without sytemd.

    Right, but systemd comes with a simple configuration files (.service files)
    which gives an easy access to these features.

systemd has bugs!

    Right, as any other software. And they are quickly fixed.

systemd developers reject patches to support platforms other than Linux:

    Ok, this is a real issue. I have no answer for that one :-)

Links:

* `Devuan <https://devuan.org/>`_: Debian fork without systemd
* http://without-systemd.org/
* https://suckless.org/sucks/systemd/

BSD systems don't use systemd but reimplemented the strict minimum systemd APIs
required by Gnome.

Slow boot: systemd-udev-settle and hdaudioC1D0
==============================================

systemd-analyze::

    [root@apu vstinner]# systemd-analyze blame
    2min 546ms systemd-udev-settle.service
       47.157s dnf-makecache.service
        5.935s NetworkManager-wait-online.service
        3.331s plymouth-quit-wait.service
        2.803s lvm2-monitor.service
        2.695s fwupd.service
        (...)

System logs::

    [root@apu vstinner]# journalctl -b
    mai 25 14:05:46 apu kernel: Linux version 5.6.12-300.fc32.x86_64 (...)
    (...)
    mai 25 14:06:53 apu systemd-udevd[626]: hdaudioC1D0: Worker [648] processing SEQNUM=3956 is taking a long time
    (...)
    mai 25 14:07:49 apu systemd[1]: systemd-udev-settle.service: Main process exited, code=exited, status=1/FAILURE
    (...)
    mai 25 14:07:49 apu systemd[1]: systemd-udev-settle.service: Failed with result 'exit-code'.
    mai 25 14:07:49 apu systemd[1]: Failed to start udev Wait for Complete Device Initialization.
    (...)
    mai 25 14:08:53 apu systemd-udevd[626]: hdaudioC1D0: Worker [648] processing SEQNUM=3956 killed
    mai 25 14:08:53 apu systemd-udevd[626]: Worker [648] terminated by signal 9 (KILL)
    mai 25 14:08:53 apu systemd-udevd[626]: hdaudioC1D0: Worker [648] failed

Blacklist ``i2c_nvidia_gpu`` kernel module::

    sudo bash -c 'echo "blacklist i2c_nvidia_gpu" >/etc/modprobe.d/blacklist-i2c-nvidia-gpu.conf'

`Kernel driver i2c-nvidia-gpu
<https://www.kernel.org/doc/html/latest/i2c/busses/i2c-nvidia-gpu.html>`_:
"driver for I2C controller included in NVIDIA Turing and later GPUs and it is
used to communicate with Type-C controller on GPUs".

