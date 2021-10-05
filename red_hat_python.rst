.. _python-rhel:

++++++++++++++++++
Red Hat and Python
++++++++++++++++++

* Red Hat contributes to Python upstream.
* `Red Hat is a Diamond sponsor of the PSF
  <https://www.python.org/psf/sponsorship/sponsors/>`_

See also: :ref:`Python in Fedora <python-fedora>`.

Python shipped with RHEL
========================

=========  ===============================================================
RHEL       Python
=========  ===============================================================
RHEL 6     Python 2.6
RHEL 7     Python 2.7
RHEL 7.7   Python 2.7.5 and Python 3.6.8
RHEL 8     Python 3.6.8, Python 3.8.0 (*), Python 3.9, Python 2.7.15 (*)
=========  ===============================================================

In RHEL 8, Python 2.7 and Python 3.8 have shorter support than RHEL, they are
shipped as app streams, not in the base operating system.

(Latest table update: 2020-06-18.)

`How to install Python 3 on Red Hat Enterprise Linux 7
<https://developers.redhat.com/blog/2018/08/13/install-python3-rhel/>`_ by Rob
Terzi (August 2018).

The Python shipped with RHEL is supported as long as RHEL: `RHEL Life Cycle
<https://access.redhat.com/support/policy/updates/errata>`_.

April 2018, `RHEL 7.5 Release Notes: Chapter 54. Deprecated Functionality
<https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/7.5_release_notes/chap-red_hat_enterprise_linux-7.5_release_notes-deprecated_functionality>`_:

    Python 2 has been deprecated: **Python 2 will be replaced with Python 3 in
    the next Red Hat Enterprise Linux** (RHEL) major release.

`How is Python 2 supported in RHEL after 2020?
<https://access.redhat.com/solutions/4455511>`_.

* no new features will be added to Python 2 in RHEL 7 and earlier.
* RHEL 8: Python 2.7 AppStream supported until June 2024.

See also `Debugging Python C extensions with GDB
<https://developers.redhat.com/articles/2021/09/08/debugging-python-c-extensions-gdb>`_
(using Python 3.9 debug build built with gcc -O0).

By default on RHEL8, python3 is ``/usr/libexec/platform-python3.6`` which
dynamically linked to ``/lib64/libpython3.6m.so.1.0``::

    $ which python3
    /usr/bin/python3

    $ ls -l /usr/bin/python3
    /usr/bin/python3 -> /etc/alternatives/python3

    $ ls -l /etc/alternatives/python3
    /etc/alternatives/python3 -> /usr/bin/python3.6

    $ ls -l /usr/bin/python3.6
    /usr/bin/python3.6 -> /usr/libexec/platform-python3.6

    $ file /usr/libexec/platform-python3.6
    /usr/libexec/platform-python3.6: ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked, ...

    $ ldd /usr/libexec/platform-python3.6
        libpython3.6m.so.1.0 => /lib64/libpython3.6m.so.1.0 (0x00007f9ad79f6000)
        ...


Python packages in RHEL
=======================

RHEL8 packages:

* python3: Python 3.6
* python2 (Module): Python 2.7

See:

* `Python in RHEL 8
  <https://developers.redhat.com/blog/2018/11/14/python-in-rhel-8/>`_
  (November 2018) by Petr Viktorin
* `What, No Python in RHEL 8 Beta?
  <https://developers.redhat.com/blog/2018/11/27/what-no-python-in-rhel-8-beta/>`_
  (November 2018) by Langdon White


Software Collections
====================

Currently supported (last update: 2018-04-23):

=============================================================================  ==============
Python version                                                                 Supported RHEL
=============================================================================  ==============
`Python27 <https://www.softwarecollections.org/en/scls/rhscl/python27/>`__     RHEL 7, RHEL 6
`Python34 <https://www.softwarecollections.org/en/scls/rhscl/rh-python34/>`__  RHEL 7, RHEL 6
`Python35 <https://www.softwarecollections.org/en/scls/rhscl/rh-python35/>`__  RHEL 7, RHEL 6
`Python36 <https://www.softwarecollections.org/en/scls/rhscl/rh-python36/>`__  RHEL 7
=============================================================================  ==============

No longer supported:

* Python33

Software Collections support: https://access.redhat.com/support/policy/updates/rhscl

Support shorter than RHEL support.

Python27 will likely be supported at least until 2020.
