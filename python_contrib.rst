.. _python-contrib:

++++++++++++++++++++++++++
My contributions to Python
++++++++++++++++++++++++++

Reports
=======

* 2017 Q3:
  `2017 Q3 (part 1) <https://vstinner.github.io/contrib-cpython-2017q3-part1.html>`_,
  `2017 Q3 (part 2) <https://vstinner.github.io/contrib-cpython-2017q3-part2.html>`_,
  `2017 Q3 (part 3) <https://vstinner.github.io/contrib-cpython-2017q3-part3.html>`_
* 2017 Q2:
  `2017 Q2 (part 1) <https://vstinner.github.io/contrib-cpython-2017q2-part1.html>`_,
  `2017 Q2 (part 2) <https://vstinner.github.io/contrib-cpython-2017q2-part2.html>`_,
  `2017 Q2 (part 3) <https://vstinner.github.io/contrib-cpython-2017q2-part3.html>`_
* `2017 Q1 <https://vstinner.github.io/contrib-cpython-2017q1.html>`_
* `2016 Q4 <https://vstinner.github.io/contrib-cpython-2016q4.html>`_
* `2016 Q3 <https://vstinner.github.io/contrib-cpython-2016q3.html>`_
* `2016 Q2 <https://vstinner.github.io/contrib-cpython-2016q2.html>`_
* `2016 Q1 <https://vstinner.github.io/contrib-cpython-2016q1.html>`_
* `2015 Q4 <https://vstinner.github.io/contrib-cpython-2015q4.html>`_
* `2015 Q3 <https://vstinner.github.io/contrib-cpython-2015q3.html>`_

Python 3.9 Contributions
========================

* New `math.nextafter()
  <https://docs.python.org/dev/library/math.html#math.nextafter>`_
  and `math.ulp()
  <https://docs.python.org/dev/library/math.html#math.ulp>`_ functions.
* New `os.waitstatus_to_exitcode()
  <https://docs.python.org/dev/library/os.html#os.waitstatus_to_exitcode>`_:
  convert a waitpid wait status to an exit code.
* New `random.randbytes()
  <https://docs.python.org/dev/library/random.html#random.randbytes>`_
  function.
* Add --with-platlibdir option to the configure script and add `sys.platlibdir
  <https://docs.python.org/dev/library/sys.html#sys.platlibdir>`_ attribute:
  used by Fedora and OpenSUSE Linux distributions to install files
  in ``/usr/lib64`` rather than ``/usr/lib``.
* Remove tons of deprecated features and deprecated a few more functions.
* `C API Changes <https://docs.python.org/dev/whatsnew/3.9.html#c-api-changes>`_:
  new functions to access structure members, private functions removed or moved
  o the internal C API. Many macros converted to static inline functions.

Python 3.8 Contributions
========================

* PEP 587: https://docs.python.org/dev/c-api/init_config.html
* New `sys.unraisablehook
  <https://docs.python.org/dev/library/sys.html#sys.unraisablehook>`_ function
* New `threading.excepthook
  <https://docs.python.org/dev/library/threading.html#threading.excepthook>`_
  function
* ``io.IOBase`` finalizer now logs close() exception using
  ``sys.unraisablehook()``
* ``_thread.start_new_thread()`` now logs thread function exception using
  ``sys.unraisablehook()``, rather than ``sys.excepthook()``, so the hook gets
  the function which created the thread and a more helpful error message.

Mentoring, bug triage permission, core developers
=================================================

I promoted the following developers as core devs:

* 2020-04-09: `Dong-hee Na
  <https://mail.python.org/archives/list/python-committers@python.org/thread/5ZZVHJHAEHT3DW5Q3X5S336KM5FE4B2C/>`_
  (`vote <https://discuss.python.org/t/vote-to-promote-dong-hee-na/3794>`__)
* 2019-09-23: `Joannah Nanjekye
  <https://mail.python.org/archives/list/python-committers@python.org/thread/DLT3RQ7W7XYGN7GH4G34DAVMWYOZIHDI/>`__
  (`vote <https://discuss.python.org/t/vote-to-promote-joannah-nanjekye-as-a-core-dev/2347>`__)
* 2019-06-16: `Paul Ganssle
  <https://mail.python.org/archives/list/python-committers@python.org/thread/YGHU7QPBTIMAU5X5K3PGJMHQQJ2XCNLY/>`__
  (`vote <https://discuss.python.org/t/vote-to-promote-paul-ganssle-as-a-core-developer/1826>`__)
* 2019-04-08: `Stéphane Wirtel
  <https://mail.python.org/pipermail/python-committers/2019-April/006677.html>`_
  (`vote <https://discuss.python.org/t/vote-to-promote-stephane-wirtel-as-a-core-dev/1044>`__)
* 2019-02-19: `Cheryl Sabella
  <https://mail.python.org/pipermail/python-committers/2019-February/006575.html>`_
  (`vote <https://discuss.python.org/t/vote-to-promote-cheryl-sabella-as-a-core-developer/862>`__)
* 2018-06-20: `Pablo Galindo Salgado
  <https://mail.python.org/pipermail/python-committers/2018-June/005621.html>`_
  (`vote <https://mail.python.org/pipermail/python-committers/2018-June/005564.html>`__)
* 2017-12-08: `Julien Palard
  <https://mail.python.org/pipermail/python-committers/2017-December/004989.html>`__
* 2016-11-21: `Xiang Zhang
  <https://mail.python.org/pipermail/python-committers/2016-November/004045.html>`__
* 2016-06-03: `Xavier de Gaye
  <https://mail.python.org/pipermail/python-committers/2016-May/003896.html>`__
* 2011-05-19: `Charles-François Natali
  <https://mail.python.org/pipermail/python-committers/2011-May/001660.html>`__

I gave the bug triage permission to:

* 2019-06-06: `Zackery Spytz
  <https://mail.python.org/archives/list/python-committers@python.org/thread/IMYXXTA2VN44ASGA33D7LVUZEWKEAUCQ/#WUZNQLX2GAETCZT62SRLL7NYDLYH7Y7F>`__
* 2019-02-22: `Andrés Delfino
  <https://mail.python.org/pipermail/python-committers/2019-February/006588.html>`__
* 2019-02-15: `Paul Ganssle
  <https://mail.python.org/pipermail/python-committers/2019-February/006567.html>`__
* 2019-02-02: `Alexey Izbyshev
  <https://mail.python.org/pipermail/python-committers/2019-February/006511.html>`_
* 2019-02-01: `Joannah Nanjekye
  <https://mail.python.org/pipermail/python-committers/2019-February/006510.html>`__
* 2018-01-18: `Pablo Galindo Salgado
  <https://mail.python.org/pipermail/python-committers/2018-January/005133.html>`__
* 2017-12-06: `Cheryl Sabella
  <https://mail.python.org/pipermail/python-committers/2017-December/004963.html>`__
* 2017-12-06: `Sanyam Khurana
  <https://mail.python.org/pipermail/python-committers/2017-December/004977.html>`__

Python Enhancement Proposals (PEP)
==================================

Lisf of my PEPs and PEPs I co-wrote.

Accepted PEPs
-------------

==========  ======  ========  =======================================================================================
PEP         Python  Status    Title
==========  ======  ========  =======================================================================================
:pep:`587`  3.8     Final     Python Initialization Configuration
:pep:`564`  3.7     Final     Add new time functions with nanosecond resolution (ex: ``time.time_ns()``)
:pep:`545`  ---     Final     Python Documentation Translations -- co-written with Juliend Palard and Naoki IANADA
:pep:`540`  3.7     Final     Add a new UTF-8 mode
:pep:`524`  3.6     Final     Make os.urandom() blocking on Linux
:pep:`509`  3.6     Final     Add a private version to dict
:pep:`475`  3.5     Final     Retry system calls failing with EINTR -- co-written with Charles-François Natali
:pep:`454`  3.4     Final     Add a new tracemalloc module to trace Python memory allocations
:pep:`446`  3.4     Final     Make newly created file descriptors non-inheritable
:pep:`445`  3.4     Final     Add new APIs to customize Python memory allocators
:pep:`418`  3.3     Final     Add monotonic time, performance counter, and process time functions
==========  ======  ========  =======================================================================================

Rejected PEPs
-------------

==========  ======  ============  ====================================================================================
PEP         Python  Status        Title
==========  ======  ============  ====================================================================================
:pep:`608`  3.9     Rejected      Coordinated Python release
:pep:`606`  3.9     Rejected      Python Compatibility Version
:pep:`546`  2.7     Rejected      Backport ssl.MemoryBIO and ssl.SSLObject to Python 2.7 -- co-written with Cory Benfield
:pep:`511`  3.6     Rejected      API for code transformers
:pep:`510`  3.6     Rejected      Specialize functions with guards
:pep:`490`  3.6     Rejected      Chain exceptions at C level
:pep:`433`  3.x     Superseded    Easier suppression of file descriptor inheritance -- supersed by my accepted PEP 446
:pep:`416`  3.3     Rejected      Add a frozendict builtin type
:pep:`410`  3.3     Rejected      Use decimal.Decimal type for timestamps
:pep:`400`  3.3     Deferred      Deprecate codecs.StreamReader and codecs.StreamWriter
==========  ======  ============  ====================================================================================

Other contributions to PEPs
---------------------------

* :pep:`460`: I wrote the `first version of the PEP 460
  <https://hg.python.org/peps/rev/7a92360bbdff>`_ (bytes % args), then
  rewritten by Antoine Pitrou, to be later superseeded by the :pep:`461`
  written by  Ethan Furman.
* :pep:`471` (os.scandir): I helped Ben Hoyt to implement, test and benchmark
  his PEP 471

Major work
==========

* Python 3.6:

  - `PEP 524: Make os.urandom() blocking on Linux
    <https://www.python.org/dev/peps/pep-0524/>`_
  - `PEP 509: Add a private version to dict
    <https://www.python.org/dev/peps/pep-0509/>`_

* Python 3.5:

  - I added the following functions:  os.get_blocking(fd) and
    os.set_blocking(fd). See `issue #22054:
    Add os.get_blocking() and os.set_blocking() functions
    <http://bugs.python.org/issue22054>`_. I added these functions because
    it's a common pattern in applications and signal.set_wakeup_fd() now
    raises an exception if the fd is blocking (I also added this check).
  - I worked with Charles-François Natali to implement the `PEP 475
    <http://www.python.org/dev/peps/pep-0475>`_: "Retry system calls failing
    with EINTR". The implementation was much more complex than expected, like
    the implementation of socket.connect() which requires many syscalls (I
    refactored Modules/socketmodule.c for that).
  - I wrote the `first version of the PEP 460
    <https://hg.python.org/peps/rev/7a92360bbdff>`_ (bytes % args), then
    rewritten by Antoine Pitrou, to be later superseeded by the `PEP 461
    <https://www.python.org/dev/peps/pep-0461/>`_ written by  Ethan Furman.
  - I helped Ben Hoyt to implement, test and benchmark his `PEP 471
    <https://www.python.org/dev/peps/pep-0471/>`_ (os.scandir)
  - On Windows, signal.set_wakeup_fd() now also supports socket handles.
  - The time.monotonic() function is now always available.
  - New API for C memory allocators to support also calloc()
  - The __name__ attribute of generator is now set from the function name,
    instead of being set from the code name. Use gen.gi_code.co_name to
    retrieve the code name. Generators also have a new __qualname__ attribute,
    the qualified name, which is now used for the representation of a generator
    (repr(gen)).
  - New private _PyTime API to handle timestamps with a resolution of 1
    nanosecond.
  - os.urandom() now uses getrandom() on Linux 3.17 and newer, and getentropy()
    on OpenBSD 5.6 and newer.
  - New private _Py_CheckFunctionResult() function to ensure that the C API is
    used correctly when calling a C function.
  - Enhance Py_FatalError()

    * Display the current Python stack if an exception was raised but the exception
      has no traceback
    * Disable faulthandler if an exception was raised (before it was only disabled
      if no exception was raised)
    * To display the current Python stack, call PyGILState_GetThisThreadState()
      which works even if the GIL was released
    * Try to flush stdout and stderr.

  - Issue #23353: complex bug related to exception handling with generators

* Python 3.4:

  - new ``tracemalloc`` module (PEP 454)
  - better handling of ``MemoryError`` exceptions
  - `PEP 446: Make newly created file descriptors non-inheritable
    <http://www.python.org/dev/peps/pep-0446/>`_

* Python 3.3:

  - new ``faulthandler`` module
  - new time functions: ``time.monotonic``, ``time.perf_counter``,
    ``time.process_time`` (PEP 418)

* Python 3.0 - 3.2

  - Major work on Unicode support to handle all platforms and all corner
    cases


April Fool
==========

* [Python-Dev] The next major Python version will be Python 8
* https://mail.python.org/pipermail/python-dev/2016-March/143603.html
* https://hg.python.org/cpython/rev/9aedec2dbc01


Old contributions to Python
===========================

Fuzzing on Python using my fuzzer "Fusil".

Accepted patches:

* 2008-07-06: `invalid ref count on locale.strcoll() error <http://bugs.python.org/issue3303>`_. Patch appliqué dans la `révision 65134 <http://svn.python.org/view?view=rev&rev=65134>`_.
* 2008-07-09: `bugs in scanstring_str() and scanstring_unicode() of _json module <http://bugs.python.org/issue3322>`_. Patch inspiré du mien commité dans la `révision 65147 <http://svn.python.org/view?rev=65147&view=rev>`_.
* 2008-07-06: `segfault on gettext(None) <http://bugs.python.org/issue3302>`_. Patch appliqué dans la `révision 65133 <http://svn.python.org/view?rev=65133&view=rev>`_.
* 2008-07-07: `bugs in _sqlite module <http://bugs.python.org/issue3312>`_. Patch appliqué dans la `révision 65040 <http://svn.python.org/view?rev=65040&view=rev>`_
* 2008-07-06: `Use Py_XDECREF() instead of Py_DECREF() in MultibyteCodec and MultibyteStreamReader <http://bugs.python.org/issue3305>`_. Patch appliqué dans `révision 65038 <http://svn.python.org/view?rev=65038&view=rev>`_
* 2008-07-07: `dlopen() error with no error message from dlerror() <http://bugs.python.org/issue3313>`_. Patch appliqué dans `rev 64976 <http://svn.python.org/view?rev=64976&view=rev>`_, `rev 64977 <http://svn.python.org/view?rev=64977&view=rev>`_ et `64978 <http://svn.python.org/view?rev=64978&view=rev>`_
* 2008-07-07: `missing lock release in BZ2File_iternext() <http://bugs.python.org/issue3309>`_. Appliqué dans le `commit 64767 <http://svn.python.org/view?rev=64767&view=rev>`_.
* 2008-07-06: `DoS when lo is negative in bisect.insort_right() / _left() <http://bugs.python.org/issue3301>`_. Appliqué dans le `commit 64845 <http://svn.python.org/view?rev=64845&view=rev>`_.
* 2008-07-06: `audioop.findmax() crashs with negative length <http://bugs.python.org/issue3306>`_. Appliqué dans le `commit 64775 <http://svn.python.org/view?rev=64775&view=rev>`_.
* 2008-07-06: `invalid call to PyMem_Free() in fileio_init() <http://bugs.python.org/issue3304>`_. Appliqué dans le `commit 64758 <http://svn.python.org/view?rev=64758&view=rev>`_
* 2007-08-13: `Improved patches for sndhdr and imghdr <http://svn.python.org/view?rev=56987&view=rev>`_
* 2007-08-10: `Fix the ctypes tests <http://svn.python.org/view?rev=56838&view=rev>`_, corrige ctypes pour le passage de str/unicode à bytes/str.
* 2007-04-10: `Segfaults quand la mémoire est épuisée <http://sourceforge.net/tracker/index.php?func=detail&aid=1697916&group_id=5470&atid=105470>`_ (rapport de bug avec patch) => patch appliqué (avec un léger changement) dans le commit `54757 (par georg.brandl) <http://svn.python.org/view?rev=54757&view=rev>`_.
* 2007-02-27: `trace.py needs to know about doctests <http://bugs.python.org/issue1429818>`_. `Patch applied the 23 Nov 2007 <http://svn.python.org/view/python/trunk/Lib/doctest.py?rev=59137&r1=59082&r2=59137>`_.
* 2006-09-06: `Bug locale.getdefaultlocale() <http://bugs.python.org/issue1553427>`_, lorsque le module _locale est absent, la fonction locale.getdefaultlocale() retourne un charset errorné avec mes locales. Corrigé dans Python 2.5.1.
* 2006-08-23: `Bug report with patch <http://sourceforge.net/tracker/index.php?func=detail&aid=1545341&group_id=5470&atid=105470>`_, La fonction setup() du module distutils refusait un tuple (au lieu d'une liste) pour la commande « register » (le patch a été retouché pour fonctionner sur Python 2.1)
* 2005-11-25: `bug report + patch <http://sourceforge.net/tracker/index.php?func=detail&aid=1366000&group_id=5470&atid=105470>`_. La méthode seek(0,2) d'un objet du module bz2 était boguée dans Python 2.4.2

Other patches (fixed as well):

* 2008-07-06: `block operation on closed socket/pipe for multiprocessing <http://bugs.python.org/issue3311>`_
* 2008-07-06: `invalid check of _bsddb creation failure <http://bugs.python.org/issue3307>`_
* 2008-07-06: `invalid object destruction in re.finditer() <http://bugs.python.org/issue3299>`_
* 2007-07-23: `Unable to register or upload project (http error 302: moved) <http://sourceforge.net/tracker/index.php?func=detail&aid=1758778&group_id=66150&atid=513503>`_
* 2007-07-17: `Problem with socket.gethostbyaddr() and KeyboardInterrupt <http://sourceforge.net/tracker/index.php?func=detail&aid=1755388&group_id=5470&atid=105470>`_
