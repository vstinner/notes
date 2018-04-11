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

* Show syslog from the most recent to the oldest logs: ``journalctl --reverse``
* Show all logs since the last boot: ``journalctl -b 0``
* List boots: ``journalctl --list-boots``
* ``tail -f /var/log/syslog``: ``journalctl -f``
* ``tail -f /var/log/syslog`` but only for apache: ``journalctl -u apache.service -f``
* Kernel logs of the current boot: ``journalctl -k`` (similar to ``dmesg`` but
  with better timestamp)
* Retain only journald logs of the past 30 days:
  ``journalctl --vacuum-time=30d``

Advantages over scattered text log files:

* Timestamps seem to be more reliable, especially for kernel logs
* Ability to display logs in the reverse order
* Ability to filter logs by service or by boot
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
