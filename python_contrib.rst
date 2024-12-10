.. _python-contrib:

++++++++++++++++++++++++++
My contributions to Python
++++++++++++++++++++++++++

GitHub links
============

* `Pull requests that I merged
  <https://github.com/search?q=is%3Apr+is%3Amerged+author%3Avstinner+archived%3Afalse+org%3Apython&type=pullrequests>`_
* `Pull requests reviewed
  <https://github.com/search?q=reviewed-by%3Avstinner+-author%3Avstinner+archived%3Afalse+org%3Apython&type=pullrequests>`_
  (excluding my own PRs)
* `Issues commented
  <https://github.com/search?q=involves%3Avstinner+org%3Apython&type=issues>`_


Python 3.13 Contributions
=========================

New Features
------------

* Add ``os.process_cpu_count()``.

Changes
-------

* ``doctest.DocTestRunner.run()`` counts the number of skipped tests.
* ``io.IOBase`` finalizer now logs close() errors.
* multiprocessing, concurrent.futures and compileall now use
  ``os.process_cpu_count()``.

Deprecate
---------

* ``ctypes.SetPointerType()``
* ``ctypes.ARRAY()``
* ``getopt`` is now soft deprecated.
* ``optparse`` is now soft deprecated.
* ``wave``: ``getmark()``, ``setmark()`` and ``getmarkers()`` methods.

Remove
------

* Remove 19 stdlib modules (PEP 594).

  * lib2to3
  * aifc
  * audioop
  * chunk
  * cgi
  * cgitb
  * crypt
  * imghdr
  * mailcap
  * nis
  * nntplib
  * ossaudiodev
  * pipes
  * sndhdr
  * spwd
  * sunau
  * telnetlib3
  * uu
  * xdrlib

* Remove many deprecated functions.
* Remove locale.resetlocale().
* Remove logging.warn() and logging.Logger.warn().
* Remove unsafe cafile, capath and cadefault parameters of
  urllib.request.urlopen().

Build Changes
-------------

* Py_TRACE_REFS build becomes ABI compatible with release and debug builds.
  This build now supports the limited C API.
* 10 extensions are now build with the limited C API.

New C API Features
------------------

Add functions:

* ``PyDict_ContainsString()``
* ``PyDict_GetItemRef()``
* ``PyDict_GetItemStringRef()``
* ``PyDict_Pop()``
* ``PyDict_PopString()``
* ``PyImport_AddModuleRef()``
* ``PyList_Clear()``
* ``PyList_Extend()``
* ``PyLong_AsInt()``
* ``PySys_AuditTuple()``
* ``PyThreadState_GetUnchecked()``
* ``PyTime_AsSecondsDouble()``
* ``PyTime_MIN`` and ``PyTime_MAX`` constants
* ``PyTime_Monotonic()``
* ``PyTime_PerfCounter()``
* ``PyTime_Time()``
* ``PyTime_t`` type
* ``PyWeakref_GetRef()``
* ``Py_HashPointer()``
* ``Py_IsFinalizing()``
* ``PyType_GetFullyQualifiedName()``
* ``PyType_GetModuleName()``

Add features:

* ``PyUnicode_FromFormat()``: add ``%T``, ``%T#``, ``%N`` and ``%N#`` formats

Other changes:

* ``PyTuple_SET_ITEM()`` and ``PyList_SET_ITEM()`` check the index with an assertion.

C API Changes
-------------

* Python.h no longer includes <ieeefp.h>, <time.h>, <sys/select.h>,
  <sys/time.h>, and <stddef.h>.

Limited C API Changes
---------------------

Add functions:

* ``PyMem_RawMalloc()``
* ``PyMem_RawCalloc()``
* ``PyMem_RawRealloc()``
* ``PyMem_RawFree()``
* ``PySys_Audit()``
* ``PySys_AuditTuple()``

Other changes:

* Undefine Py_BUILD_CORE, Py_BUILD_CORE_BUILTIN and Py_BUILD_CORE_MODULE
  macros.

Deprecate C API
---------------

* ``Py_UNICODE`` and ``PY_UNICODE_TYPE`` types
* ``PySys_ResetWarnOptions()``
* ``Py_GetExecPrefix()``
* ``Py_GetPath()``
* ``Py_GetPrefix()``
* ``Py_GetProgramFullPath()``
* ``Py_GetProgramName()``
* ``Py_GetPythonHome()``
* ``PyImport_ImportModuleNoBlock()``
* ``PyWeakref_GetObject()``
* ``PyWeakref_GET_OBJECT()``

Remove C API
------------

* Remove many private C API: functions starting with ``_Py`` or ``_PY`` prefix.
* ``PyCFunction_Call()``
* ``PyEval_CallFunction()``
* ``PyEval_CallMethod()``
* ``PyEval_CallObject()``
* ``PyEval_CallObjectWithKeywords()``
* ``PySys_AddWarnOption()``
* ``PySys_AddWarnOptionUnicode()``
* ``PySys_AddXOption()``
* ``PySys_HasWarnOptions()``
* ``PySys_SetArgv()``
* ``PySys_SetArgvEx()``
* ``PySys_SetPath()``
* ``Py_SetPath()``
* ``Py_SetProgramName()``
* ``Py_SetPythonHome()``
* ``Py_SetStandardStreamEncoding()``
* ``_Py_SetProgramFullPath()``
* ``PyEval_InitThreads()``
* ``PyEval_ThreadsInitialized()``
* ``PyEval_AcquireLock()``
* ``PyEval_ReleaseLock()``
* ``_PyObject_FastCall()``
* ``Include/cpython/pytime.h`` header file.
* ``_PyInterpreterState_Get()``


Python 3.12 Contributions
=========================

New Features
------------

* Build: Add ``COMPILEALL_OPTS`` variable in ``Makefile``

Changes
-------

* Invalid escape sequence in strings now generates ``SyntaxWarning``,
  instead of ``DeprecationWarning``

Remove
------

* ``distutils`` package
* ``Tools/demo/`` directory
  (`12 demos <https://twitter.com/VictorStinner/status/1576959791087616000>`__)
* ``Tools/scripts/`` directory: remove 70 scripts
* ``ElementTree.Element.copy()`` (pure Python implementation)
* ``FTP_TLS.ssl_version``
* ``gzip.GzipFile.filename``
* ``io.OpenWrapper``, ``_pyio.OpenWrapper``
* ``locale.format()``
* ``ssl.RAND_pseudo_bytes()``
* ``ssl.match_hostname()``
* ``ssl.wrap_socket()``
* ``zipimport``: Remove ``find_loader()`` and ``find_module()`` methods
* Remove the ``keyfile``, ``certfile`` and ``check_hostname`` parameters in
  modules: ftplib, http.client, imaplib, poplib and smtplib.

C API: New Features
-------------------

* ``PyFrame_GetVar()``
* ``PyFrame_GetVarString()``

C API: Deprecate
----------------

* ``Py_DebugFlag``
* ``Py_VerboseFlag``
* ``Py_QuietFlag``
* ``Py_InteractiveFlag``
* ``Py_InspectFlag``
* ``Py_OptimizeFlag``
* ``Py_NoSiteFlag``
* ``Py_BytesWarningFlag``
* ``Py_FrozenFlag``
* ``Py_IgnoreEnvironmentFlag``
* ``Py_DontWriteBytecodeFlag``
* ``Py_NoUserSiteDirectory``
* ``Py_UnbufferedStdioFlag``
* ``Py_HashRandomizationFlag``
* ``Py_IsolatedFlag``
* ``Py_LegacyWindowsFSEncodingFlag``
* ``Py_LegacyWindowsStdioFlag``
* ``Py_FileSystemDefaultEncoding``
* ``Py_FileSystemDefaultEncodeErrors``
* ``Py_UTF8Mode``

C API: Remove
-------------

* ``token.h`` header file
* ``PyUnicode_InternImmortal()``
* ``SSTATE_INTERNED_IMMORTAL``


Python 3.11 Contributions
=========================

New features
------------

* Add ``-P`` command line option, ``PYTHONSAFEPATH`` environment variable and
  ``sys.flags.safe_path``: don't prepend a potentially unsafe path to
  ``sys.path``.

Changes
-------

* On Unix, if the ``sem_clockwait()`` function is available,
  ``threading.Lock.acquire()`` uses the monotonic clock for the timeout.
* ``math.nan`` is now always available
* C11 compiler and C99 ``<math.h>`` are now required to build Python

Remove
------

* ``binhex`` module
* ``binascii``: remove ``a2b_hqx()``, ``b2a_hqx()``, ``rlecode_hqx()`` and
  ``rldecode_hqx()``
* ``float.__set_format__()``
* ``"U"`` flag of ``open()``, ``io.open()`` and ``codecs.open()``

Deprecate
---------

* ``locale.getdefaultlocale()``
* ``locale.resetlocale()``
* ``mailcap`` module
* ``lib2to3`` package

C API: New Features
-------------------

* ``PyThreadState_EnterTracing()``, ``PyThreadState_LeaveTracing()``
* ``PyFloat_Pack2()``, ``PyFloat_Pack4()``, ``PyFloat_Pack8()``
* ``PyFloat_Unpack2()``, ``PyFloat_Unpack4()``, ``PyFloat_Unpack8()``
* ``PyConfig.safe_path``

C API: Changes
--------------

* PEP 670: Convert many macros to static inline functions.
* Py_TYPE() and Py_SIZE() can no longer be used as l-value
* Move 8 non-limited header files to ``Include/cpython/``
* Frame API is now directly part of ``<Python.h>``, like ``PyFrame_GetBack()``

C API: Deprecate
----------------

* ``PySys_AddWarnOption()``
* ``PySys_AddWarnOptionUnicode()``
* ``PySys_AddXOption()``
* ``PySys_HasWarnOptions()``
* ``PySys_SetArgv()``
* ``PySys_SetArgvEx()``
* ``PySys_SetPath()``
* ``Py_SetPath()``
* ``Py_SetProgramName()``
* ``Py_SetPythonHome()``
* ``Py_SetStandardStreamEncoding()``
* ``_Py_SetProgramFullPath()``

C API: Limited C API
--------------------

* The limited C API no longer includes ``<stdlib.h>``, ``<stdio.h>``,
  ``<errno.h>`` and ``<string.h>``.
* Remove ``PyWeakref_GET_OBJECT()``
* Remove ``PyUnicode_CHECK_INTERNED()``

C API: Remove
-------------

* ``HAVE_PY_SET_53BIT_PRECISION``
* ``PyHeapType_GET_MEMBERS()``
* ``Py_ADJUST_ERANGE1()``
* ``Py_ADJUST_ERANGE2()``
* ``Py_FORCE_DOUBLE()``
* ``Py_OVERFLOWED()``
* ``Py_SET_ERANGE_IF_OVERFLOW()``
* ``Py_SET_ERRNO_ON_MATH_ERROR()``
* ``Py_UNICODE_COPY()``
* ``Py_UNICODE_FILL()``
* ``eval.h`` header
* ``pystrhex.h`` header

Python 3.10 Contributions
=========================

New features
------------

* Add ``sys.orig_argv`` attribute
* Add ``sys.stdlib_module_names`` attribute
* Add new ``./configure`` options:

  * ``--without-static-libpython``
  * ``--with-wheel-pkg-dir=PATH``

* ``faulthandler`` now lists third party C extensions on a crash
* ``faulthandler`` now detects if a fatal error occurs during a GC collection

Changes
-------

* Optimize ``python3 -m module`` startup time: import less modules.
* Static methods (@staticmethod) are now callable as regular functions
  module: ``collections.MutableMapping`` must be replaced with
  ``collections.abc.MutableMapping``.
* At Python exit, if a callback registered with ``atexit.register()`` fails,
  its exception is now logged
* Remove distutils ``bdist_wininst`` command
* Remove deprecated aliases to Abstract Base Classes from the collections

New C API features
------------------

* Add ``PyConfig.orig_argv`` member
* Add new functions:

  * ``PyModule_AddObjectRef()``
  * ``Py_Is()``
  * ``Py_IsFalse()``
  * ``Py_IsNone()``
  * ``Py_IsTrue()``
  * ``Py_NewRef()``
  * ``Py_XNewRef()``

* Add new ``Py_TPFLAGS_DISALLOW_INSTANTIATION`` and
  ``Py_TPFLAGS_IMMUTABLETYPE`` type flags

C API changes
-------------

* ``Py_REFCNT()`` can no longer be used as a l-value
* Deprecate ``PyUnicode_InternImmortal()``
* Remove ``_Py_CheckRecursionLimit`` variable
* Remove header files:

  * ``Python-ast.h``
  * ``asdl.h``
  * ``ast.h``
  * ``symtable.h``

* Remove functions:

  * ``PyAST_Compile()``
  * ``PyAST_CompileEx()``
  * ``PyAST_CompileObject()``
  * ``PyAST_Validate()``
  * ``PyArena_AddPyObject()``
  * ``PyArena_Free()``
  * ``PyArena_Malloc()``
  * ``PyArena_New()``
  * ``PyFuture_FromAST()``
  * ``PyFuture_FromASTObject()``
  * ``PyOS_InitInterrupts()``
  * ``PyParser_ASTFromFile()``
  * ``PyParser_ASTFromFileObject()``
  * ``PyParser_ASTFromFilename()``
  * ``PyParser_ASTFromString()``
  * ``PyParser_ASTFromStringObject()``
  * ``Py_SymtableString()``

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
* Add ``./configure --with-platlibdir`` option and add `sys.platlibdir
  <https://docs.python.org/dev/library/sys.html#sys.platlibdir>`_ attribute:
  used by Fedora and OpenSUSE Linux distributions to install files
  in ``/usr/lib64`` rather than ``/usr/lib``.
* Remove many deprecated features and deprecate some functions.
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

Python 3.7 Contributions
========================

* New `Python UTF-8 Mode <https://docs.python.org/dev/library/os.html#python-utf-8-mode>`_:
  ``-X utf8`` option and ``PYTHONUTF8=1`` env var, PEP 540.
* New `Python Development Mode
  <https://docs.python.org/dev/library/devmode.html>`_:
  ``-X dev`` and ``PYTHONDEVMODE`` env var
* New time functions with nanosecond resolution, PEP 564:

  * ``time.clock_gettime_ns()``
  * ``time.clock_settime_ns()``
  * ``time.monotonic_ns()``
  * ``time.perf_counter_ns()``
  * ``time.process_time_ns()``
  * ``time.time_ns()``

* New sys.getandroidapilevel() function on Android.
* C API:

  * New ``PyTraceMalloc_Track()`` and ``PyTraceMalloc_Untrack()`` functions for
    numpy.

Python 3.6 Contributions
========================

* Add `PYTHONMALLOC
  <https://docs.python.org/dev/using/cmdline.html#envvar-PYTHONMALLOC>`_ env
  var: it becomes possible to use debug hooks on a Python release build.
* New ``ast.Constant`` AST node.
* ``faulthandler`` installs a handler for Windows exceptions.
* Implement `PEP 509: Add a private version to dict
  <https://www.python.org/dev/peps/pep-0509/>`_
* Add ``os.getrandom()`` function, `PEP 524: Make os.urandom() blocking on
  Linux <https://www.python.org/dev/peps/pep-0524/>`_.
* ``subprocess``: destructor emits a ``ResourceWarning`` if the process is
  still running.
* ``tracemalloc`` supports racing memory allocations in multiple different address
  spaces.
* ``warnings``: new ``source`` parameter, used to display the traceback where
  an object was allocated when displaying a ``ResourceWarning``.
* Optimize ASCII, Latin1 and UTF-8 decoders and encoders when handling
  undecodable bytes and unencodable characters for common error handlers
  (ignore, replace, surrogateescape, surrogatepass).
* ``PyMem_Malloc()`` uses ``pymalloc`` allocator, rater than ``malloc()``.
* Remove ``make touch``: add ``make regen-all``.

Python 3.5 Contributions
========================

* Add ``os.scandir()``: collaborative work with Ben Hoyt.
* ``os.walk()`` is 7x to 20x faster on Windows, thanks to os.scandir()
* Implement PEP 475 with  Charles-François Natali: Retry system calls failing
  with EINTR. Refactor ``Modules/socketmodule.c``: add ``sock_call()`` helper
  function which retries a syscall and recomputes the timeout.
* asyncio:

  * Add ``create_task()``, ``get_debug()``, ``set_debug()`` and ``is_closed()``
    functions.
  * Queue: new ``join()`` and ``task_done()`` methods.
  * proactor event loop supports SSL, collaborative work with Antoine Pitrou

* ``time.monotonic()`` is always available.
* ``os.urandom()`` uses ``getrandom()`` on Linux
* New ``os.get_blocking()`` and ``os.set_blocking()`` functions.
* ``signal.set_wakeup_fd()`` accepts Windows socket handle
* socket functions use a monotonic clock
* Fix socket.sendall() timeout
* C API:

  * New ``PyMem_Calloc()`` function.
  * New ``Py_DecodeLocale()`` and ``Py_EncodeLocale()`` functions.
  * New private ``_PyTime`` API to handle nanosecond timestamps.
  * Enhance ``Py_FatalError()``
  * New private ``_Py_CheckFunctionResult()`` function.

Python 3.4 Contributions
========================

* New ``tracemalloc`` module:
  PEP 454 – Add a new tracemalloc module to trace Python memory allocations
* Implement `PEP 446: Make newly created file descriptors non-inheritable
  <http://www.python.org/dev/peps/pep-0446/>`_. New functions:

  * ``os.get_inheritable()``, ``os.set_inheritable()``
  * ``os.get_handle_inheritable()``, ``os.set_handle_inheritable()``
  * ``socket.socket.get_inheritable()``, ``socket.socket.set_inheritable()``

* Implement PEP 445 – Add new APIs to customize Python memory allocators
* UTF-8, UTF-16 and UTF-32 codecs reject surrogates: collaborative work with
  Kang-Hao (Kenny) Lu and Serhiy Storchaka.
* New ``os.cpu_count()`` function ( (Contributed by Trent Nelson, Yogesh Chaudhari,
  Victor Stinner, and Charles-François Natali)
* select.devpoll: add fileno(), close() methods and closed attribute.
* ``PyUnicode_FromFormat()`` supports width and precision specifications for
  ``%s``, ``%A``, ``%U``, ``%V``, ``%S``, and ``%R``.
  (Collaborative work with Ysj Ray.)
* Better handling of ``MemoryError`` exceptions

Python 3.3 Contributions
========================

* New ``faulthandler`` module
* ssl: add ``RAND_bytes()`` and ``RAND_pseudo_bytes()``
* subprocess: command strings can now be bytes objects on posix platforms
* time: add functions, PEP 418:

  * ``clock_getres()``
  * ``clock_gettime()``
  * ``clock_settime()``
  * ``get_clock_info()``
  * ``monotonic()``
  * ``perf_counter()``
  * ``process_time()``

Python 3.2 Contributions
========================

* Python’s import mechanism can now load modules installed in directories with
  non-ASCII characters in the path name. This solved an aggravating problem
  with home directories for users with non-ASCII characters in their usernames.
* New os.getenvb() function and os.environb mapping

Python 3.1 Contributions
========================

* int: add ``bit_length()`` method. I wrote a first implementation, Mark
  Dickinson completed my implementation.

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

* 2020-11-13: `Hai Shi
  <https://mail.python.org/archives/list/python-committers@python.org/thread/MLO4LWMOT5DW6JD7RCHDS5GPLNWHXCNE/>`__
* 2019-06-06: `Zackery Spytz
  <https://mail.python.org/archives/list/python-committers@python.org/thread/IMYXXTA2VN44ASGA33D7LVUZEWKEAUCQ/>`__
* 2019-02-22: `Andrés Delfino
  <https://mail.python.org/pipermail/python-committers/2019-February/006588.html>`__
* 2019-02-15: `Paul Ganssle
  <https://mail.python.org/pipermail/python-committers/2019-February/006567.html>`__
  (is now a core dev)
* 2019-02-02: `Alexey Izbyshev
  <https://mail.python.org/pipermail/python-committers/2019-February/006511.html>`_
* 2019-02-01: `Joannah Nanjekye
  <https://mail.python.org/pipermail/python-committers/2019-February/006510.html>`__
  (is now a core dev)
* 2018-01-18: `Pablo Galindo Salgado
  <https://mail.python.org/pipermail/python-committers/2018-January/005133.html>`__
  (is now a core dev)
* 2017-12-06: `Cheryl Sabella
  <https://mail.python.org/pipermail/python-committers/2017-December/004963.html>`__
  (is now a core dev)
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
:pep:`757`  3.14    Accepted  C API to import-export Python integers
:pep:`741`  3.14    Final     Python Configuration C API
:pep:`737`  3.13    Final     C API to format a type fully qualified name
:pep:`670`  3.11    Final     Convert macros to functions in the Python C API
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

Total: 12 accepted PEPs.

Draft PEPs
----------

===========  ======  ==========================================================
PEP          Python  Title
===========  ======  ==========================================================
:pep:`743`   3.14    Add Py_COMPAT_API_VERSION to the Python C API
===========  ======  ==========================================================

Rejected PEPs
-------------

===========  ======  ============  ====================================================================================
PEP          Python  Status        Title
===========  ======  ============  ====================================================================================
:pep:`8015`  ---     Rejected      Organization of the Python community
:pep:`756`   3.14    Withdrawn     Add PyUnicode_Export() and PyUnicode_Import() C functions
:pep:`674`   3.11    Deferred      Disallow using macros as l-values
:pep:`620`   3.10    Withdrawn     Hide implementation details from the C API
:pep:`608`   3.9     Rejected      Coordinated Python release
:pep:`606`   3.9     Rejected      Python Compatibility Version
:pep:`546`   2.7     Rejected      Backport ssl.MemoryBIO and ssl.SSLObject to Python 2.7 -- co-written with Cory Benfield
:pep:`511`   3.6     Rejected      API for code transformers
:pep:`510`   3.6     Rejected      Specialize functions with guards
:pep:`490`   3.6     Rejected      Chain exceptions at C level
:pep:`433`   3.x     Superseded    Easier suppression of file descriptor inheritance -- supersed by my accepted PEP 446
:pep:`416`   3.3     Rejected      Add a frozendict builtin type
:pep:`410`   3.3     Rejected      Use decimal.Decimal type for timestamps
:pep:`400`   3.3     Deferred      Deprecate codecs.StreamReader and codecs.StreamWriter
===========  ======  ============  ====================================================================================

Total: 13 rejected, deferred or superseded PEPs.

Other contributions to PEPs
---------------------------

* :pep:`460`: I wrote the `first version of the PEP 460
  <https://hg.python.org/peps/rev/7a92360bbdff>`_ (bytes % args), then
  rewritten by Antoine Pitrou, to be later superseeded by the :pep:`461`
  written by  Ethan Furman.
* :pep:`471` (os.scandir): I helped Ben Hoyt to implement, test and benchmark
  his PEP 471

Commits
=======

Number of commits with the name "Victor Stinner", per year, from 2010 to
2022-11-02:

* 2022: 348 (on going)
* 2021: 260
* 2020: 524
* 2019: 467
* 2018: 306
* 2017: 420 (migration to Git on GitHub)
* 2016: 612
* 2015: 731
* 2014: 820
* 2013: 630
* 2012: 261
* 2011: 1027 (migration to Mercurial)
* 2010: 696

Total: 7 102 commits

Old reports (2015-2017)
=======================

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

Statistics
==========

* `CPython Insights: Contributors
  <https://github.com/python/cpython/graphs/contributors>`_
* `GitHub High Score (cpython)
  <https://leereilly.net/github-high-scores/?python/cpython>`_
