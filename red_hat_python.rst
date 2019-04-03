++++++++++++++++++
Red Hat and Python
++++++++++++++++++

* Red Hat contributes to Python upstream.
* `Red Hat is a Diamond sponsor of the PSF
  <https://www.python.org/psf/sponsorship/sponsors/>`_

Packages
========

RHEL8
-----

* python3: Python 3.6
* python2 (Module): Python 2.7

See:

* `Python in RHEL 8
  <https://developers.redhat.com/blog/2018/11/14/python-in-rhel-8/>`_
  (November 2018) by Petr Viktorin
* `What, No Python in RHEL 8 Beta?
  <https://developers.redhat.com/blog/2018/11/27/what-no-python-in-rhel-8-beta/>`_
  (November 2018) by Langdon White


Python shipped with RHEL
========================

=========  ===========
RHEL       Python
=========  ===========
RHEL 6     Python 2.6
RHEL 7     Python 2.7
Next RHEL  Python 3
=========  ===========

The Python shipped with RHEL is supported as long as RHEL.
RHEL support: https://access.redhat.com/support/policy/updates/errata

April 2018, `RHEL 7.5 Release Notes: Chapter 54. Deprecated Functionality
<https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/7.5_release_notes/chap-red_hat_enterprise_linux-7.5_release_notes-deprecated_functionality>`_:

    Python 2 has been deprecated: **Python 2 will be replaced with Python 3 in
    the next Red Hat Enterprise Linux** (RHEL) major release.


How to install Python 3 on RHEL 7
=================================

https://developers.redhat.com/blog/2018/08/13/install-python3-rhel/


Software Collections
====================

Currently supported (last document update: 2018-04-23):

=============================================================================  ==============
Python version                                                                 Supported RHEL
=============================================================================  ==============
`Python27 <https://www.softwarecollections.org/en/scls/rhscl/python27/>`__     RHEL 7, RHEL 6
`Python35 <https://www.softwarecollections.org/en/scls/rhscl/rh-python34/>`__  RHEL 7, RHEL 6
`Python35 <https://www.softwarecollections.org/en/scls/rhscl/rh-python35/>`__  RHEL 7, RHEL 6
`Python36 <https://www.softwarecollections.org/en/scls/rhscl/rh-python36/>`__  RHEL 7
=============================================================================  ==============

No longer supported:

* Python33

Software Collections support: https://access.redhat.com/support/policy/updates/rhscl

Support shorter than RHEL support.

Python27 will likely be supported at least until 2020.


.. _python-in_fedora:

Python in Fedora
================

* `Fedora Loves Python <https://fedoralovespython.org/>`_
* `Fedora Developer: Multiple Python interpreters
  <https://developer.fedoraproject.org/tech/languages/python/multiple-pythons.html>`_
* `Fedora EPEL <https://fedoraproject.org/wiki/EPEL>`_

See also :ref:`Fedora <fedora>`.


Fedora packages
===============

In April 2019, 3 branches are supported:

* f29: Fedora 29 (stable)
* f39: Fedora 30 (beta)
* master: Fedora Rawhide (unstable)

There are the following packages for Python:

* `python2 <https://src.fedoraproject.org/rpms/python2/>`_: Python 2.7
* `python34 <https://src.fedoraproject.org/rpms/python34/>`_: Python 3.4
* `python35 <https://src.fedoraproject.org/rpms/python35/>`_: Python 3.5
* `python36 <https://src.fedoraproject.org/rpms/python36/>`_: Python 3.6
* `python3 <https://src.fedoraproject.org/rpms/python3/>`_: Python 3.7
* `python38 <https://src.fedoraproject.org/rpms/python38/>`_: Python 3.8

Old stuff:

* Old branches: f27 (Fedora 27), f26 (Fedora 26), ... (``python`` package has
  branches up to f10: Fedora 10)
* The `python <https://src.fedoraproject.org/rpms/python/>`_ package is now
  dead. It has been renamed to ``python2``.
