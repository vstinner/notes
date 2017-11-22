.. _cpython:

+++++++
CPython
+++++++

See also :ref:`Compile CPython on Windows <cpython-windows>`.

Developer mode
==============

https://mail.python.org/pipermail/python-ideas/2016-March/039314.html

Enable all runtime debug checks in strict mode::

   PYTHONMALLOC=debug python3.6 -Wd -bb -X faulthandler script.py


CPython infra
=============

Python infrastructure
---------------------

* http://infra.psf.io/
* https://status.python.org/ Status of services maintained by the Python infra
  team
* https://github.com/python/psf-chef/

  - `doc/nodes.rst
    <https://github.com/python/psf-chef/blob/master/doc/nodes.rst>`_
  - `doc/roles.rst
    <https://github.com/python/psf-chef/blob/master/doc/roles.rst>`_

* https://github.com/python/psf-salt/
* PSF pays a full-time sysadmin to maintain the Python infra: XXX
* https://www.python.org/psf/league/
* Managed services: http://infra.psf.io/overview/#details-of-various-services
* http://www.pythontest.net/ used by the test suite, see
  https://github.com/python/pythontestdotnet/

Services used by unit tests
---------------------------

* pythontest.net services:

  * `pythontestdotnet <https://github.com/python/pythontestdotnet>`_: source of
    pythontest.net (resources used for Python test suite).
  * test_urllib2net: http://www.pythontest.net/index.html#frag, tcp/80 (HTTP)
  * FTP: ftp://www.pythontest.net/README
  * Copies of unicode text files like http://www.pythontest.net/unicode/EUC-CN.TXT
  * test_hashlib test files like http://www.pythontest.net/hashlib/blake2b.txt
  * test_httplib: self-signed.pythontest.net, tcp/443 (HTTPS)
  * test_robotparser: http://www.pythontest.net/elsewhere/robots.txt
  * test_socket: испытание.pythontest.net

* snakebite.net::

    # Testing connect timeout is tricky: we need to have IP connectivity
    # to a host that silently drops our packets.  We can't simulate this
    # from Python because it's a function of the underlying TCP/IP stack.
    # So, the following Snakebite host has been defined:
    blackhole = resolve_address('blackhole.snakebite.net', 56666)

    # Blackhole has been configured to silently drop any incoming packets.
    # No RSTs (for TCP) or ICMP UNREACH (for UDP/ICMP) will be sent back
    # to hosts that attempt to connect to this address: which is exactly
    # what we need to confidently test connect timeout.

    # However, we want to prevent false positives.  It's not unreasonable
    # to expect certain hosts may not be able to reach the blackhole, due
    # to firewalling or general network configuration.  In order to improve
    # our confidence in testing the blackhole, a corresponding 'whitehole'
    # has also been set up using one port higher:
    whitehole = resolve_address('whitehole.snakebite.net', 56667)

* news.trigofacile.com:

  * Used by test_nntplib
  * NNTP (tcp/119) and and NNTP/SSL (tcp/563)
  * Server administrator: julien@trigofacile.com

* ipv6.google.com:

  * test_ssl uses it to test IPv6: HTTP (tcp/80) and HTTPS (tcp/443)

* sha256.tbs-internet.com:

  * test_ssl uses it to test x509 certificate signed by SHA256: HTTPS (tcp/443)

Package Index (PyPI)
--------------------

* https://pypi.org/ "Warehouse", the new Python Package Index,

  - https://github.com/pypa/warehouse

* https://pypi.python.org/ "Python Cheeseshop", the old Python Package Index
* Python CDN: http://infra.psf.io/services/cdn/

cpython GitHub project
----------------------

* https://github.com/python/cpython/
* GitHub uses mention-bot: https://github.com/facebook/mention-bot

  * https://github.com/mention-bot/how-to-unsubscribe
  * userBlacklist, userBlacklistForPR in `CPython .mention-bot
    <https://github.com/python/cpython/blob/master/.mention-bot>`_
  * Adding you GitHub login to userBlacklistForPR stops the mention bot from
    mentioning anyone on your PRs.

* https://github.com/python/core-workflow/tree/master/cherry_picker/

Misc
----

* http://bugs.python.org/ Bug tracker (modified instance of Roundup)

  * https://pypi.python.org/pypi/roundup
  * Meta bug tracker: http://psf.upfronthosting.co.za/roundup/meta/
    (bug in the bug tracker software)

* Mailing lists: https://mail.python.org/mailman/listinfo

  - python-dev
  - python-ideas
  - python-list
  - lot of Special Interest Groups (SIG)
  - etc.

* http://buildbot.python.org/

  * `CPython 3.6
    <http://buildbot.python.org/all/waterfall?category=3.6.stable&category=3.6.unstable>`_
  * `CPython 3.x (master)
    <http://buildbot.python.org/all/waterfall?category=3.x.stable&category=3.x.unstable>`_
  * `Custom builders
    <https://docs.python.org/devguide/buildbots.html#custom-builders>`_
  * `buildmaster-config
    <https://github.com/python/buildmaster-config/tree/master/master>`_
    (configuration)
  * `Fork of BuildBot running on buildbot.python.org
    <https://github.com/python/buildbot/>`_

* GitHub CLA bot: XXX

Documentation
-------------

* https://docs.python.org/ Python online documentation
* https://github.com/python/docsbuild-scripts/
* Mirror: http://python.readthedocs.io/en/latest/ Still use the old Mercurial repository.
* https://www.python.org/dev/peps/pep-0545/ i18n doc


Python developer mode
=====================

https://mail.python.org/pipermail/python-ideas/2016-March/039314.html

Strict developer mode::

    PYTHONMALLOC=debug python3.6 -Werror -bb -X faulthandler script.py

Developer mode::

    PYTHONMALLOC=debug python3.6 -Wd -b -X faulthandler script.py

* Show ``DeprecationWarning`` and ``ResourceWarning warnings``: ``python -Wd``
* Show ``BytesWarning`` warning: ``python -b``
* Enable ``faulthandler`` to get a Python traceback on segfault and fatal
  errors: ``python -X faulthandler``
* Debug hooks on Python memory allocators: ``PYTHONMALLOC=debug``
* Enable Python assertions (assert) and set ``__debug__`` to ``True``: remove
  (or just ignore) -O or -OO command line arguments

See also ``PYTHONASYNCIODEBUG=1`` for asyncio.


Embedded libraries
==================

Update dependencies: https://github.com/python/cpython-source-deps/blob/master/README.rst

See my `external_versions.py
<https://github.com/vstinner/misc/blob/master/cpython/external_versions.py>`_
script: external version of embedded libraries from CPython source code
(locally).

On security branches, some dependencies are outdated because no more macOS nor
Windows installer is built. It was decided to not upgrade outdated zlib 1.2.5
in Python 3.3.7, since it's specific to Windows, and no Windows user is
expected to build his/her own Python 3.3 anymore.

* ``Modules/_ctypes/libffi/``: copy of `libffi <https://sourceware.org/libffi/>`_

  * Removed from Python 3.7: https://bugs.python.org/issue27979

* ``Modules/_ctypes/libffi_osx/``: `libffi <https://sourceware.org/libffi/>`_ for macOS?

  * Version: ``grep PACKAGE_VERSION Modules/_ctypes/libffi_osx/include/fficonfig.h``
  * Python 2.7-3.6 uses libffi 2.1

* ``Modules/_ctypes/libffi_msvc/``: `libffi <https://sourceware.org/libffi/>`_
  for Windows (for Microsoft Visual Studio)?

  * Version: second line of ``Modules/_ctypes/libffi_msvc/ffi.h``
  * Python 2.7-3.6 use libffi 2.0 beta, copied from ctypes-0.9.9.4 in 2006

* ``Modules/expat/``: copy of `libexpat <https://github.com/libexpat/libexpat/>`_

  * ``./configure --with-system-expat``
  * Rationale: https://mail.python.org/pipermail/python-dev/2017-June/148287.html
  * Used on Windows and macOS, Linux distributions use system libexpat
  * Version: search for ``XML_MAJOR_VERSION`` in ``Modules/expat/expat.h``
  * Script to update it: see attached script to https://bugs.python.org/issue30947
  * Recent update: https://bugs.python.org/issue30947
  * Python 2.7, 3.3-3.6 use libexpat 2.2.1

* ``Modules/zlib/``: copy of `zlib <https://zlib.net/>`_

  * Version: ``ZLIB_VERSION`` in ``Modules/zlib/zlib.h``
  * Only used on Windows (system zlib is used on macOS and Linux)
  * Python zlib module not built if system zlib is older than 1.1.3
  * Script to update it: XXX
  * Recent update: https://bugs.python.org/issue29169
  * Python 2.7, 3.4 and 3.5, 3.6 use zlib 1.2.11
  * Python 3.3 uses zlib 1.2.5: https://github.com/python/cpython/pull/3108

* ``Modules/_decimal/libmpdec/``: copy of `libmpdec <http://www.bytereef.org/mpdecimal/>`_

  * Option: ``./configure --with-system-libmpdec``
  * Included since Python 3.3 for _decimal
  * Maintained by Stefan Krah
  * Version: ``MPD_VERSION`` in ``Modules/_decimal/libmpdec/mpdecimal.h``
  * Used on all platforms
  * Script to update: XXX
  * Recent update: https://bugs.python.org/issue26621
  * Python 3.6 uses libmpdec 2.4.2 (released at february 2016)
  * Python 3.4 and 3.5 uses libmpdec 2.4.1
  * Python 3.3 uses libmpdec 2.4.0

* Windows and macOS installers include OpenSSL (binary library)

  * Windows version: search for ``openssl-`` in ``PCbuild/get_externals.bat``
  * macOS version: search for ``openssl-`` in ``Mac/BuildScript/build-installer.py``
  * See: http://python-security.readthedocs.io/ssl.html#openssl-versions
  * See: https://www.python.org/dev/peps/pep-0543/

* Windows and macOS installers include `SQLite <https://www.sqlite.org/>`_

  * Recent update: https://bugs.python.org/issue28791
  * macOS: search for ``SQLite`` in ``Mac/BuildScript/build-installer.py``
  * Windows: search for ``sqlite-`` in ``PCbuild/get_externals.bat``

See also `cpython-bin-deps <https://github.com/python/cpython-bin-deps>`_
and `cpython-source-deps <https://github.com/python/cpython-source-deps>`_.


Prashanth Raghu's documentation
===============================

* `Internals of CPython 2.7
  <https://intopythoncom.files.wordpress.com/2017/04/internalsofcpython2-7.pdf>`_
* `Internals of CPython 3.6
  <https://intopythoncom.files.wordpress.com/2017/04/internalsofcpython3-6-1.pdf>`_
* `Advanced Internals of CPython 3.6
  <https://intopythoncom.files.wordpress.com/2017/04/merged.pdf>`_


Contribute to CPython: where should you start?
==============================================

Documentation:

* https://devguide.python.org/
* http://cpython-core-tutorial.readthedocs.io/en/latest/

How can you start? Where? That's an hard question. CPython is old and widely
used: any change must be carefully discussed to remain Python homogenous.
For bug fixes, the most complex part is the backward compatibility.

It's very hard to find "easy issue". First, just **watch** the current activity
to get some ideas.

* To start, the best is maybe to look at recent commits to see what is
  currently done to get some ideas:
  https://github.com/python/cpython/commits/master
* Look also at active bugs: see https://bugs.python.org/ homepage, and maybe
  the second and third pages
* You may also look at ideas currently discussed on the
  https://mail.python.org/mailman/listinfo/python-ideas mailing list

Contribute to CPython? What is CPython? CPython is made of many parts:

* CPython source code: basically made of 50% Python and 50% C code
* Build system: complex tools to build Python on all platforms, Visual
  Studio project for Windows
* Windows and macOS installer
* 233,000 lines of documentation written with Sphinx
* Documentation translated to multiple languages: french, japanese, and other
  languages
* Bug tracker: bugs.python.org which has its own "meta" bug tracker for bugs in
  the bug tracker :-)
* GitHub project: pull requests, host the Git repository
* Travis CI to run the test suite on Linux and check the documentation
* AppVeyor CI to run the test suite on Windows
* Buildbot master and many workers to run the test suite as post-commit on
  many variables architectures and operating systems

There are also many things around Python:

* Devguide: documentation of the CPython development workflow
* python-dev and python-committers mailing lists
* #python-dev IRC channel
* PyPI

Contributing to CPython is hard and it can take up to 2 years until your work
is released. Are you sure that CPython itself is the best project for you?
Depending on your interests and skills, you may enjoy better to contribute
to another popular project like Django or requests.

Contributing to CPython is harder because CPython developers require a very
high quality for contributions: every change must be carefully documented,
tested and implemented. The implementation can take several rounds until it
reachs the expected quality and respect a long list of requirements.

Ok, I understand and I am well aware of all these things. But I want to
contribute, how should I start?

* Bug triage: complete bug report to adjust the title, complete the
  description, identify impacted Python version and impacted platforms,
  help to reproduce the bug, or even help to analyze and find the **root bug**.

* Review pull requests: https://github.com/python/cpython/pulls/

  * Make sure that a change is carefully documented. For example, behaviour
    changes and enhancements must have the "..  versionchanged:: x.y" markup in
    the documentation of the module.
    New features must be have the ".. versionadded:: x.y" tag and maybe also
    documented in "What's New in Python X.Y?" documentation.
  * The NEWS entry and commit message must first explain the solved problem,
    then maybe explain the change itself. While the commit message can be
    technical and very detailed, the NEWS entry should be short and written
    for end-users who don't care of technical details.
  * Every change must be tested: exceptions are rare and should usually be
    justified. Example of exception which doesn't have to be justified: changes
    only impacting the documentation, changes fixing a typo in a comment.
  * The backward compatibility is very important. A change must be carefully
    reviewed to make sure that it doesn't break the backward compatibility.
    If it does break it, the change must be discussed with enough people
    to make sure that there is a smooth transition plan.
  * Feature removals require a DeprecationWarning in Python version N to remove
    it in version N+1. It's common that a feature is kept longer to avoid
    breaking the world just being a developer wants the perfection.
    Python developers must be pragmatic: balance between perfection and
    usability, very hard choices should be made and usually it takes a a long
    to time to discuss them :-)
  * While Python 2 end of line is near (2020), Python 3 changes which make
    writing code working on Python 2 and Python 3 harder are usually rejected.

* Propose to write a bugfix change (a pull request) for an existing bug report.
  This task is very hard since usually if a bug report doesn't have a patch,
  it's because there is a disagrement on the bug itself, or because the bugfix
  is very hard to implement.


Supported platforms
===================

PEP 11 lists removed platforms:

* MS-DOS
* Python 3.4: VMS, OS/2, Windows 2000
* Python 3.7: IRIX

Windows:

* Windows XP supported in Python 2.7, not supported in Python 3.6
* Windows 2000 support dropped in Python 3.4

Well supported platforms on Python 3.6 and 2.7:

* Linux
* Windows: XXX min version?
* macOS: XXX min version?
* FreeBSD

Tested by Travis CI and buildbots.

Supported platform with best effort support:

* Android API 24
* OpenBSD
* NetBSD
* Solaris, OpenIndiana
* AIX

Platforms not supported officially:

* Cygwin
* MinGW
* HP-UX
