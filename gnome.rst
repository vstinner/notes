+++++++++++++++++
GNOME and Wayland
+++++++++++++++++

My articles:

* https://vstinner.github.io/debug-hybrid-graphics-issues-linux.html
* https://vstinner.github.io/graphics-bugs-firefox-gnome.html

Customize GNOME
===============

* Settings > Keyboard > Create a custom shortcut: ALT+E runs gnome-terminal
* Settings > Keyboard > Navigate > Change window: set shortcut to ALT+TAB,
  it removes the shortcut of "Change application" which groups windows of the
  same application

Fedora IRC channel
==================

Join `#fedora-desktop on irc.gnome.org <irc://irc.gnome.org/fedora-desktop>`_.

GNOME
=====

`GNOME <https://www.gnome.org/>`_ desktop made of multiple components:

* `Mutter <https://en.wikipedia.org/wiki/Mutter_(software)>`_: compositor
  supportting Xorg and Wayland, use **Clutter** library
* `libinput <https://wayland.freedesktop.org/libinput/doc/latest/>`_:
  library that provides a full input stack for display servers and other
  applications that need to handle input devices provided by the kernel.
  Try ``sudo libinput list-devices`` and ``sudo libinput debug-events``
  commands.
* `GJS <https://gitlab.gnome.org/GNOME/gjs/wikis/Home>`_: Javascript Bindings
  for Gnome, use Mozilla SpiderMonkey. Provide "gjs" program which can run
  Javascript in the command line.
* `Xwayland <https://wayland.freedesktop.org/xserver.html>`_: X server using
  Wayland compositor
* `GNOME Shell <https://en.wikipedia.org/wiki/GNOME_Shell>`_ is the GNOME
  desktop environment. It is written in C and JavaScript as a plugin for
  Mutter. It's the **gnome-shell** program. Main features:

  * Handle inputs using **libinput** library
  * Wayland compositor using **Mutter** (as a library)
  * Run shell extensions written in Javascript using **GJS** (as a library)

Mutter spawns Xwayland and sets the ``DISPLAY`` environment variable which
is inherited by child processes: all graphical applications started in GNOME.


Wayland
=======

This section is unrelated to Hybrid Graphics, but useful to debug graphics
issues.

Do I use Wayland?
-----------------

Is "type wayland" found in the loginctl session status? ::

    $ loginctl session-status|grep Service:
    Service: gdm-password; type wayland; class user

Is ``WAYLAND_DISPLAY`` environment variable set? ::

    $ env|grep -E '^(XDG_SESSION_TYPE|WAYLAND_DISPLAY|DISPLAY)'
    XDG_SESSION_TYPE=wayland
    WAYLAND_DISPLAY=wayland-0
    DISPLAY=:0

Is Xwayland running? ::

    $ ps ax|grep Xwayland
     1956 tty2     Sl+    6:38 /usr/bin/Xwayland :0 ...

In GNOME Shell, Mutter spawns Xwayland and sets the ``DISPLAY`` environment
variable which is inherited by child processes: all graphical applications
started in GNOME.


Is this application using Wayland or Xorg?
------------------------------------------

``xprop`` or ``xwininfo`` program can be in Wayland to check if an application
is using Xorg or Wayland: the mouse cursor becomes a cross only and only if the
application is used Xorg (X11 API).

``xlsclients`` command lists programs using XWayland.

Opt-in for Wayland
------------------

To opt-in for Wayland support in **Firefox** and Thunderbird, set ``MOZ_ENABLE_WAYLAND=1`` environment variable.

For example, I put the following line into ``/etc/environment`` to run Firefox
with Wayland::

    MOZ_ENABLE_WAYLAND=1

When a Wayland compositor is running, Gtk applications prefer Wayland by
default. In that case, you can opt-in for X11 by seting ``GDK_BACKEND=x11``
environment variable.


Wayland and Xorg
================

Debug: https://fedoraproject.org/wiki/How_to_debug_Wayland_problems

See also: https://fedoraproject.org/wiki/How_to_debug_Firefox_problems

Environment to opt-in for Wayland support::

    export GDK_BACKEND=wayland

To run Firefow with Firefox, edit ``/etc/environment`` to add the line::

    MOZ_ENABLE_WAYLAND=1

Get GPUs::

    $ lspci|grep VGA
    00:02.0 VGA compatible controller: Intel Corporation HD Graphics 530 (rev 06)
    01:00.0 VGA compatible controller: NVIDIA Corporation GM107GLM [Quadro M1000M] (rev a2)

Get OpenGL GPU::

    $ glxinfo|grep -E 'Device|rendering'
    direct rendering: Yes
        Device: Mesa DRI Intel(R) HD Graphics 530 (Skylake GT2)  (0x191b)

Get screen resolution::

    $ xrandr
    Screen 0: minimum 320 x 200, current 3840 x 1080, maximum 8192 x 8192
    XWAYLAND0 connected 1920x1080+0+0 (normal left inverted right x axis y axis) 510mm x 290mm
       1920x1080     59.96*+
    XWAYLAND1 connected 1920x1080+1920+0 (normal left inverted right x axis y axis) 480mm x 270mm
       1920x1080     59.96*+

Get screen DPI (96x96 in this example)::

    $ xdpyinfo | grep -B 2 resolution
    screen #0:
      dimensions:    3840x1080 pixels (1016x286 millimeters)
      resolution:    96x96 dots per inch

Check if an application is using Xorg or Wayland in Wayland: run ``xprop``,
the mouse cursor becomes a cross only for Xorg appplications.

Hybrid Graphics (2 GPUs)
------------------------

Disable Nouveau driver::

    sudo grubby --update-kernel=ALL --args="modprobe.blacklist=nouveau"

Fedora 30, add an argument to all GRUB kernel configurations::

    sudo grubby --update-kernel=ALL --args="xdg.force_integrated=0"

Disable switcheroo-control (don't run it anymore at startup)::

    sudo systemctl stop switcheroo-control.service
    sudo systemctl disable switcheroo-control.service

My Lenovo P50 has 2 GPU, one slow integrated Intel GPU and one fast Nvidia GPU.
There is a `switcheroo-control <https://github.com/hadess/switcheroo-control>`_
D-Bus service to check if the system has 2 GPUs.

Linux kernel ``vgaswitcheroo``::

    $ sudo cat /sys/kernel/debug/vgaswitcheroo/switch
    0:IGD:+:Pwr:0000:00:02.0
    1:DIS: :DynPwr:0000:01:00.0

* IGD: Integrated Graphics Device
* DIS: DIScrete graphics device
* "+": active card

Links:

* https://www.kernel.org/doc/html/latest/gpu/vga-switcheroo.html
* https://help.ubuntu.com/community/HybridGraphics

DBus::

    gdbus introspect --system --dest net.hadess.SwitcherooControl --object-path /net/hadess/SwitcherooControl
    ...
    interface net.hadess.SwitcherooControl {
      ...
      properties:
        readonly b HasDualGpu = true;
    };

See `bumblebee <https://docs.fedoraproject.org/en-US/quick-docs/bumblebee/>`_.

Launch an application with Nvidia GPU from a terminal::

    DRI_PRIME=1 firefox

Firefox:

* Go to about:support and search for the Graphics section
* WebGL https://webglreport.com/ ::

    Unmasked Vendor: nouveau
    Unmasked Renderer: NV117


Xorg BadWindow issue
====================

Set ``GDK_SYNCHRONIZE`` environment variable to debug such issue::

    The program 'gnome-shell' received an X Window System error.
    This probably reflects a bug in the program.
    The error was 'BadWindow (invalid Window parameter)'.
      (Details: serial 352312 error_code 3 request_code 18 (core protocol) minor_code 0)
      (Note to programmers: normally, X errors are reported asynchronously;
       that is, you will receive the error a while after causing it.
       To debug your program, run it with the GDK_SYNCHRONIZE environment
       variable to change this behavior. You can then get a meaningful
       backtrace from your debugger if you break on the gdk_x_error() function.)

* https://gitlab.gnome.org/GNOME/gnome-shell/issues/760
* https://gitlab.gnome.org/GNOME/gnome-shell/issues/1230
* https://gitlab.gnome.org/GNOME/gnome-shell/issues/661
* https://gitlab.gnome.org/GNOME/gnome-shell/issues/627
* https://gitlab.gnome.org/GNOME/gnome-shell/issues/496
* https://gitlab.gnome.org/GNOME/gnome-shell/issues/375
* https://gitlab.gnome.org/GNOME/gnome-shell/issues/213
* Ubuntu: https://bugs.launchpad.net/ubuntu/+source/gnome-shell/+bug/1821427
* Fedora: https://bugzilla.redhat.com/show_bug.cgi?id=712612


My GPU bugs on Fedora
=====================

My bugs:

* 2020-01-28, Intel IGP: `i915 0000:00:02.0: GPU HANG: ecode 9:1:0x00000000, hang on rcs0
  <https://gitlab.freedesktop.org/drm/intel/issues/1053>`_
* 2020-01-23: `d_alloc: list_add corruption. next->prev should be prev (ffff930b5d4b6ca0), but was 0000000000000000. (next=ffff930beff5b690)
  <https://bugzilla.redhat.com/show_bug.cgi?id=1794350>`_ (Intel IGP?)

My laptop Lenovo P50 has two GPUs:

* Integrated Graphics Device: Intel IGP (Intel HD Graphics 530)
* Discrete Graphics Device: NVIDIA GPU (NVIDIA Quadro M1000M)

See `Debug Hybrid Graphics issues on Linux
<https://vstinner.github.io/debug-hybrid-graphics-issues-linux.html>`_.


Wayland copy/paste in command line
==================================

Commands::

    $ wl-copy bla
    $ wl-paste
    bla

Fedora: ``dnf install wl-clipboard``.
