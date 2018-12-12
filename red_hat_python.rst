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
