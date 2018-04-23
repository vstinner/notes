++++++++++++++++++
Red Hat and Python
++++++++++++++++++

* Red Hat contributes to Python upstream.

System Python
=============

System Python are /usr/bin/pythonX.Y binaries.

=========  ===========
RHEL       Python
=========  ===========
RHEL 6     Python 2.6
RHEL 7     Python 2.7
Next RHEL  Python 3
=========  ===========

System Python is supported as long as RHEL.

Python 2.7 has been deprecated in RHEL 7.5. The next major RHEL version
will replace Python 2 with Python 3 (only provide Python 3).

RHEL support: https://access.redhat.com/support/policy/updates/errata

Software Collections
====================

Currently supported (last document update: 2018-04-23):

============================================================================  ==============
Python version                                                                Supported RHEL
============================================================================  ==============
`Python27 <https://www.softwarecollections.org/en/scls/rhscl/python27/>`_     RHEL 7, RHEL 6
`Python35 <https://www.softwarecollections.org/en/scls/rhscl/rh-python34/>`_  RHEL 7, RHEL 6
`Python35 <https://www.softwarecollections.org/en/scls/rhscl/rh-python35/>`_  RHEL 7, RHEL 6
`Python36 <https://www.softwarecollections.org/en/scls/rhscl/rh-python36/>`_  RHEL 7
============================================================================  ==============

No longer supported:

* Python33

Software Collections support: https://access.redhat.com/support/policy/updates/rhscl

Support shorter than RHEL support.

Python27 will likely be supported at least until 2020.
