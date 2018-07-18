+++++++++++++++++++++++
Single file application
+++++++++++++++++++++++

There are different projects to install an application as a single file:

=============================================   ===================================================
Project                                         Application Store
=============================================   ===================================================
`Flatpak <https://www.flatpak.org/>`_           `Flathub <https://flathub.org/>`_
`Snaps (Snapcraft) <https://snapcraft.io/>`_    `Snapcraft Store <https://snapcraft.io/store>`_
`AppImage <https://appimage.org/>`_             `AppImageHub <https://appimage.github.io/apps/>`_
=============================================   ===================================================

The first use case is to easy install graphical applications ("desktop GUI
apps"), but Snaps is also designed to package services (server daemons).

Comparison written by AppImage (not objective): `AppImage: Similar Projects
<https://github.com/AppImage/AppImageKit/wiki/Similar-projects>`_.

Features:

* "Shared Runtime": don't duplicate files on disk, share memory between
  processes, whenever possible
* Easy and atomic upgrade
* App Store (centralized or distributed repositories)
* Sandboxing for security
* Number of packaged applications
* Don't depend on the Linux distribution: installable on Debian, OpenSUSE,
  Fedora, etc.

Supporters:

* Flatpak: Red Hat, Endless, Gnome
* Snapcraft: Canonical (Ubuntu)
* AppImage: OpenSUSE

Applications
============

Example of applications that you can find packaged:

* Popular open source applications:

  * Audacity
  * GIMP
  * LibreOffice
  * VLC

* Popular commercial applications:

  * Spotify
  * Skype
  * Steam
  * Slack

Linux technologies
==================

"Applications as a single file" reuse many features which have been pushed by
containers to the Linux kernel and userspace to isolate "services" (daemon
servers):

* CGroups
* Namespaces for everything: user identifiers, process identifiers, filesystem
  root, network, etc.
* Sandboxing

  * Linux SECCOMP
  * `bubblewrap <https://github.com/projectatomic/bubblewrap>`_:
    "Unprivileged sandboxing tool": used by docker, systemd-nspawn and flatpak
    for example.

Flatpak
=======

Flatpak is made of 3 things:

* software deployment
* package management
* application virtualization

Links:

* `Flatpak – a history
  <https://blogs.gnome.org/alexl/2018/06/20/flatpak-a-history/>`_
  by Alexander Larsson (June, 2018)
* `Using Flatpak with Python
  <https://www.loganasherjones.com/2018/05/using-flatpak-with-python/>`_
  by Logan Jones (May 2018)
* Portals: ???

* `winepak <https://www.winepak.org/>`_: Flatpak-ing Microsoft Windows
  applications with Wine.

  * BattleNet
  * Overwatch
  * StarCraft2
  * WoW
  * Fortnite
  * League of Legends
  * etc.

* Old names of Flatpak: "Glick" (followed by "Glick2"), then "xdg-app".
* Old name of "BubbleWrap" (sandbox used internally by Flatpak):
  "xdg-app-helper".

See also:

* `OSTree <https://ostree.readthedocs.io/>`_
* `Project Atomic <https://www.projectatomic.io/>`_
* `CoreOS <https://coreos.com/>`_

Snap
====

* Contributors must sign a CLA.

AppImage
========

* Old AppImage name: "klik".

Misc
====

* Click?
* Docker: different usage
* Virtual Machine (VirtualBox, virt-manager, qemu, etc.): different usage
* systemd:

  * systemd-nspawn
  * machinectl
  * casync? (`blog article
    <http://0pointer.net/blog/casync-a-tool-for-distributing-file-system-images.html>`_)
  * `portable services (blog article)
    <http://0pointer.net/blog/walkthrough-for-portable-services.html>`_
  * `dynamic users with systemd (blog article)
    <http://0pointer.net/blog/dynamic-users-with-systemd.html>`_

* macOS uses `.dmg files <https://en.wikipedia.org/wiki/Apple_Disk_Image>`_:
  one file per application.
* Nix/Guix: closer to regular package manages (multiple files), but can be
  used without being root.
* `0install <http://0install.net/>`_
* Image signature?
* `Revisiting How We Put Together Linux Systems
  <http://0pointer.net/blog/revisiting-how-we-put-together-linux-systems.html>`_
  by Lennart Poettering (Sept 2014)
* https://en.wikipedia.org/wiki/Application_virtualization
