.. _contrib:

++++++++++++++++++++++++++++++++++
My Contributions to Free Softwares
++++++++++++++++++++++++++++++++++

See also my :ref:`projects <projects>` and my :ref:`contributions to Python <python-contrib>`.

Contributions in 2016
=====================

* Fedora Cloud Image, bug reports:

  * https://bugzilla.redhat.com/show_bug.cgi?id=1405391
  * https://fedorahosted.org/fedora-websites/ticket/415

* testrepository

 * PR `Fix two ResourceWarning warnings
   <https://github.com/testing-cabal/testrepository/pull/25>`_
 * Issue `Subprocesses pipes (stdout, stderr) are not explicitly closed:
   ResourceWarning warnings are logged
   <https://github.com/testing-cabal/testrepository/issues/26>`_

* pip

  * Issue: `pip should use the distro module: platform.linux_distribution()
    has been deprecated in Python 3.5
    <https://github.com/pypa/pip/issues/3823>`_
  * PR: `Fix a ResourceWarning in setuptools_build
    <https://github.com/pypa/pip/pull/3824>`_

* setuptools

  * `Don't use deprecated 'U' flag to read manifest
    <https://github.com/pypa/setuptools/pull/623>`_

* python-json-patch

  * `Use inspect.signature() on Python 3
    <https://github.com/stefankoegl/python-json-patch/pull/52>`_
  * `Add tox.ini
    <https://github.com/stefankoegl/python-json-patch/pull/51>`__

* numpy

  * `Use PyMem_RawMalloc on Python 3.4 and newer
    <https://github.com/numpy/numpy/pull/7404>`_
  * `Assertion error when running tests on Python 3.6 compiled in debug mode
    <https://github.com/numpy/numpy/issues/7399>`_
  * https://github.com/numpy/numpy/issues/7360

* eventlet:

  * PR #303: `Add hubs.default_clock and use time.monotonic
    <https://github.com/eventlet/eventlet/pull/303>`_
  * Bug report: `Python 3: wsgi doesn't handle correctly partial write of
    socket send() when using writelines()
    <https://github.com/eventlet/eventlet/issues/295>`_


Contributions in 2015
=====================

* monotonic

  * `clock_gettime() is not thread-safe
    <https://github.com/atdt/monotonic/pull/12>`_
  * `Don't use CLOCK_MONOTONIC_RAW #13
    <https://github.com/atdt/monotonic/pull/13>`_
  * both merged into monotonic 0.5 released at 2015-12-27

* routes:

  - `Add tox.ini <https://github.com/bbangert/routes/pull/55>`__
  - `Fix BytesWarning in Mapper.generate() <https://github.com/bbangert/routes/pull/56>`_

* pep8: `fix BytesWarning on Python 3 <https://github.com/PyCQA/pep8/pull/459>`_
* eventlet: Python 3 patches

  -
    PR #275: `Issue #274: Fix GreenSocket.recv_into() <https://github.com/eventlet/eventlet/pull/275>`_.
    Issue: `On Python 3, sock.makefile('rb').readline() doesn't handle blocking
    errors correctly <https://github.com/eventlet/eventlet/issues/274>`_
  - PR #257: `Fix GreenFileIO.readall() for regular file
    <https://github.com/eventlet/eventlet/pull/257>`_
  - `Issue #248: eventlet.monkey_patch() on Python 3.4 makes stdout
    non-blocking <https://github.com/eventlet/eventlet/issues/248>`_: pull
    request `Fix GreenFileIO.write()
    <https://github.com/eventlet/eventlet/pull/250>`_
  - `Issue #230: Fix patcher.original, don't load a module twice when eventlet
    monkey-patched is not used
    <https://github.com/eventlet/eventlet/pull/231>`_
  - `tox 1.8 or newer is required
    <https://github.com/eventlet/eventlet/pull/225>`_
  - `Fix threading monkey-patching on Python 3.4
    <https://github.com/eventlet/eventlet/pull/224>`_
  - `Fix threading.Condition with monkey-patching on Python 3.3 and newer #187
    <https://github.com/eventlet/eventlet/pull/187>`_
    on Python 3.3 and newer when monkey patching is used)


Contributions in 2014
=====================

* pip: `Fix issue #1433: parse requirements in markers #1472 <https://github.com/pypa/pip/pull/1472>`_.
  Since pip 6.0, it is possible to write ``futures; python_version < '2.7'`` in
  requirements.txt. Feature very useful to specify requirements specific to
  Python 2, or only for an old Python version.
* eventlet: Python 3 patches

  - `Fix monkey-patched os.open(): add dir_fd parameter #170
    <https://github.com/eventlet/eventlet/pull/170>`_
  - `enhance socketpair code in tpool #167
    <https://github.com/eventlet/eventlet/pull/167>`_
  - `Fix monkey_patch() on Python 3 #168
    <https://github.com/eventlet/eventlet/pull/168>`_

* Mercurial bug reports:

  - `Bug 4516 - Rename information lost after merge+edit+commit amend
    <http://bz.selenic.com/show_bug.cgi?id=4516>`_
  - `Bug 4306 - histedit blocked if i exchange and edit a commit (unknown revision / no node)
    <http://bz.selenic.com/show_bug.cgi?id=4306>`_


Old Work (2004-2008)
====================

First, see my :ref:`old projects <old-projects>`.

Accepted patches in other projects
----------------------------------

* 2008-05-08, *PyPy*: modules pwd et syslog implémentés avec ctypes (bon maintenant j'ai un compte Subversion chez PyPy, alors j'accepte mes propres contrib' :-))
* 2008-03-05, *PyPy*: `_locale module implementation in ctypes <https://codespeak.net/issue/pypy-dev/issue361>`_
* 2008-02-21, *PyPy*: `resource module implementation using ctypes <https://codespeak.net/issue/pypy-dev/issue358>`_
* 2007-12-03, *Apache*: `Fix XSS in error page #413 <http://issues.apache.org/bugzilla/show_bug.cgi?id=44014>`_. Voir le `commit dans Subversion <http://svn.apache.org/viewvc/httpd/httpd/trunk/modules/http/http_protocol.c?r1=594839&r2=600645&diff_format=h>`_.
* 2006-09-06, *PyPy*: `Corrige le module codec pour la casse des charsets <http://codespeak.net/pipermail/pypy-svn/2006-September/015612.html>`_ (pour être compatible avec CPython)
* 2006-08-21, *urwid*: `Patch ''setuptools'' <http://lists.excess.org/pipermail/urwid/2006-August/000294.html>`_ (appliqué dans la version 0.9.6)
* 2006-04-27, *Dia* : http://bugzilla.gnome.org/show_bug.cgi?id=334771 Patch qui corrige un plantage alétoire lors du "dégroupage" d'un objet] (appliqué dans Dia 0.95)
* 2005-06-16, *Gnome* : `Patch pour libgnomeui <http://bugzilla.gnome.org/show_bug.cgi?id=307885>`_. Nautilus utilisait 500 Mo de mémoire pour générer une miniature d'une image SVG de 28 Ko ! Mon patch limite au maximum le gaspillage de mémoire. (appliqué dans la version 2.11)

Pending patches
---------------

* 2008-07-07, *PHP*: `count_chars() crashs if both arguments are the same reference <http://bugs.php.net/bug.php?id=45441>`_
* 2007-08-16, *yui*: `container css: "cursor: pointer" instead of "cursor: hand" <http://sourceforge.net/tracker/index.php?func=detail&aid=1775306&group_id=165715&atid=836476>`_


INL/EdenWall
============

During my work at INL/EdenWall, I contributed to many open source softwares:

* 2007, iptables: `#7080: Don't silenty exit on failure to open
  /proc/net/{ip,ip6}_tables_names
  <http://svn.netfilter.org/cgi-bin/viewcvs.cgi?rev=7080&amp;view=rev>`_
* libnfnetlink: `#6741: fix autogen.sh (sh syntax for string comparaison)
  <http://svn.netfilter.org/cgi-bin/viewcvs.cgi?rev=6741&amp;view=rev>`_
* libnetfilter_conntrack: `#6721: fix a crash on setting the counters of a
  conntrack, implement getter for the ATTR_USE attribute
  <http://svn.netfilter.org/cgi-bin/viewcvs.cgi?rev=6721&amp;view=rev>`_
* 2006, libnetfilter_conntrack: `#6719: Fix XML output syntax
  <http://svn.netfilter.org/cgi-bin/viewcvs.cgi?rev=6719&amp;view=rev>`_
* libnfnetlink: `#6718: Initialize callback structure
  <http://svn.netfilter.org/cgi-bin/viewcvs.cgi?rev=6718&amp;view=rev>`_
* libnetfilter_conntrack: `#6716: Fix new API test program (replace ntohs by
  htons), introduce NFCT_O_PLAIN flag
  <http://svn.netfilter.org/cgi-bin/viewcvs.cgi?rev=6716&amp;view=rev>`_
* gcrypt (july 2006): `Fix missing initializer warning in gcrypt.h
  <http://marc.info/?l=gcrypt-devel&amp;m=115273044813499&amp;w=2>`_
* `Microoptimize destruction of unused statitically initialized mutexes
  <http://marc.info/?l=gcrypt-devel&amp;m=115273103732416&amp;w=2>`_
* 2005, (lxml library) `Invalid use of xmlIO: crash on xmlCharEncCloseFunc()
  <https://bugs.launchpad.net/lxml/+bug/227259>`_
* (CPython) `Bugfix for crashes on low-memory conditions
  <http://svn.python.org/view?rev=54757&amp;view=rev>`_
* (Python ctypes) `ctypes: wrong calling convention for _string_at
  <http://bugs.python.org/issue3900>`_. See `issue #3554
  <http://bugs.python.org/issue3554>`_, 3900 was a duplicate of this bug :-/
* `PHP <http://www.php.net/>`_: `bug report #42817
  <http://bugs.php.net/bug.php?id=42817>`_
* `Dia <http://www.gnome.org/projects/dia/>`_: `Bug #334771 (Ungroup crashes)
  <http://bugzilla.gnome.org/show_bug.cgi?id=334771>`_ fixed
* `libc <http://www.gnu.org/software/libc/>`_: Bug report made by Victor
  Stinner: `vfprintf() segfault with multibyte string and long precision
  <http://sources.redhat.com/bugzilla/show_bug.cgi?id=4438>`_. Ulrich Drepper
  fixed the bug: see `vfprintf patch v1.136
  <http://sources.redhat.com/cgi-bin/cvsweb.cgi/libc/stdio-common/vfprintf.c.diff?r1=1.135&amp;r2=1.136&amp;cvsroot=glibc&amp;f=h>`_

Security vulnerabilities:

* 2007-05-22: `CVE-2007-2754
  <http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2007-2754>`_: FreeType
  Integer Overflow in TT_Load_Simple_Glyph()
* 2007-05-11: `CVE-2007-2650
  <http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2007-2650>`_: ClamAV OLE2
  Parser Denial of Service
* 2007-05-10: `CVE-2007-2645
  <http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2007-2645>`_: Libexif
  Integer Overflow Vulnerability in exif_data_load_data_entry()


Fuzzing
=======

Thanks to my project `Fusil <http://fusil.readthedocs.org/>`_, I found and
sometimes fixed many bugs in various softwares. See the `list of crashes found
by Fusil <http://fusil.readthedocs.org/crash_list.html>`_.


Bug reports
===========

Fixed:

* 2007-05-07, *ImageMagick*: `Crash in EXIF parser with invalid IFD count <http://www.imagemagick.org/discourse-server/viewtopic.php?f=3&t=9033>`_. The file also crash gwenview application.
* 2007-04-30, *libc*: `vfprintf() segfault with multibyte string and long precision <http://sources.redhat.com/bugzilla/show_bug.cgi?id=4438>`_.

 - Le bug a été corrigé par Ulrich Drepper :  `patch vfprintf v1.136 <http://sources.redhat.com/cgi-bin/cvsweb.cgi/libc/stdio-common/vfprintf.c.diff?r1=1.135&r2=1.136&cvsroot=glibc&f=h>`_
 - `Rapport de bug Fedora Core <https://bugzilla.redhat.com/bugzilla/show_bug.cgi?id=238406>`_
 - `Rapport de bug Debian <http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=421555>`_

* 2007-04-28, *FreeType*: `Another bug in TTF (cmap) <http://lists.gnu.org/archive/html/freetype-devel/2007-04/msg00043.html>`_, voir le `patch sfnt/sfobjs.c version 1.128 <http://cvs.savannah.nongnu.org/viewcvs/freetype2/src/sfnt/sfobjs.c?root=freetype&r1=1.127&r2=1.128>`_
* 2007-04-27, *FreeType*: `Bug in fuzzed TTF file <http://lists.gnu.org/archive/html/freetype-devel/2007-04/msg00041.html>`_. Voir le `patch (dans CVS) <http://cvs.savannah.nongnu.org/viewcvs/freetype2/src/truetype/ttgload.c?root=freetype&r1=1.177&r2=1.178>`_.

Open:

* 2008-02-21: *PyPy*, `large-file support and file.seek() <https://codespeak.net/issue/pypy-dev/issue357>`_
* 2008-01-28: *Firefox*, `Venkman crashs on profiling after clearing profile data <https://bugzilla.mozilla.org/show_bug.cgi?id=414451>`_
* 2008-01-28: *command-not-found*, `phpize is missing from program.d database <https://bugs.launchpad.net/ubuntu/+source/command-not-found/+bug/186626>`_
* 2007-10-01: *PHP*, `buffer under- and overflow on clone(null)+array_push() <http://bugs.php.net/bug.php?id=42817>`_

 - `Diff sur zend_vm_execute.h <http://cvs.php.net/viewvc.cgi/ZendEngine2/zend_vm_execute.h?r1=1.193&r2=1.195&sortby=date>`_
 - Tests de non regression : `bug36071.phpt <http://cvs.php.net/viewvc.cgi/ZendEngine2/tests/bug36071.phpt?view=log>`_, `bug42817.phpt <http://cvs.php.net/viewvc.cgi/ZendEngine2/tests/bug42817.phpt?view=log>`_, `bug42818.phpt <http://cvs.php.net/viewvc.cgi/ZendEngine2/tests/bug42818.phpt?view=log>`_

* 2007-07-05, *ClamAV*:

  - `#561: OLE2: Long (slow) loop in ole2_walk_property_tree() with huge prop_index value <https://wwws.clamav.net/bugzilla/show_bug.cgi?id=561>`_
  - `#560: bitset_realloc() is not atomic <https://wwws.clamav.net/bugzilla/show_bug.cgi?id=560>`_ (avec patch et testcase)
  - `#559: OLE2: Allocate too much memory with invalid file <https://wwws.clamav.net/bugzilla/show_bug.cgi?id=559>`_ (avec patch et testcase)

* 2007-04-18, *ClamAV*: `Bug in OLE2 file parser <http://news.gmane.org/gmane.comp.security.virus.clamav.devel/cutoff=2853>`_ (DoS found with fuzzing), dans bugzilla: `Bug #466 <https://wwws.clamav.net/bugzilla/show_bug.cgi?id=466>`_ (fermé au public)
* 2007-04-20, *ImageMagick*: `Bug report in TGA and XCF files <http://www.imagemagick.org/discourse-server/viewtopic.php?f=3&t=8956>`_ (DoS found with fuzzing)
* 2005-06-16, *gdb* : `Display libc function names instead of address? <http://sources.redhat.com/ml/gdb/2005-06/msg00166.html>`_

Other
=====

* I contributed to some articles on the french Wikipedia, like:
  `Sténographie <http://fr.wikipedia.org/wiki/Sténographie>`_.
