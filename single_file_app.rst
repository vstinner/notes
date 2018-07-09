+++++++++++++++++++++++
Single file application
+++++++++++++++++++++++

There are different projects to install an application as a single file:

* `Flatpak <https://www.flatpak.org/>`_: `Flathub <https://flathub.org/>`_ (App Store)
* `Snapcraft (Snap) <https://snapcraft.io/>`_: `Snapcraft Store <https://snapcraft.io/store>`_ (App Store)
* `AppImage <https://appimage.org/>`_: No App Store?

Others:

* Click?
* Genymotion?
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

Features:

* "Shared Runtime"
* Upgrade
* App Store (centralized or distributed repositories)
* Sandboxing for security
* Number of packaged applications

Supporters:

* Flatpak: Red Hat, Gnome
* Snapcraft: Canonical (Ubuntu)
* AppImage: OpenSUSE


Flatpak
=======

* `Flatpak – a history
  <https://blogs.gnome.org/alexl/2018/06/20/flatpak-a-history/>`_
  by Alexander Larsson (June, 2018)
* `Using Flatpak with Python
  <https://www.loganasherjones.com/2018/05/using-flatpak-with-python/>`_
  by Logan Jones (May 2018)
* Portals: ???
* Commercial applications:

  * Spotify
  * Skype
  * Steam

* `winepak <https://www.winepak.org/>`_: Flatpak-ing Microsoft Windows
  applications with Wine.

  * BattleNet
  * Overwatch
  * StarCraft2
  * WoW
  * Fortnite
  * League of Legends
  * etc.
