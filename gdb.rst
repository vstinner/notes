.. _gdb:

+++++++++++++++++
GDB: GNU debugger
+++++++++++++++++


.. image:: debugging.png
   :alt: Debugging
   :target: http://www.monkeyuser.com/2018/debugging/

gdb commands
============

* ``info sharedlibrary``: list loaded shared libraries (see also
  ``sharedlibrary`` command to explicitly load shared libraries)
* ``info sources``: list code source files

Debug methodolody
=================

The first step is to debug is to find a reliable or highly reliable scenario to
reproduce the bug. In the worst case, it can take several days to get such
reliable scenario :-/


Code bisection
--------------

If a bug occurred recently and it didn't exist in previous versions, it's
called a regression and it should be easier to debug. If the code is tracked
by a Version Control System (VCS like Git or Mercurial), you can "bisect"
the source code history to find the changeset introducing the bug. Git and
Mercurial have a builtin ``bisect`` command:

* :ref:`hg bisect <hg-bisect>`
* git bisect

The best is to have a reliable script reproducing the bug which returns
0 on success (test succeeded, no bug) or non-zero exit code (test failed,
bug). Example of shell script::

    make || exit 125
    ./python -m test -v test_sys

``make || exit 125`` fails with the exit code 125 if the compilation fails.
It's useful to skip a revision if the project cannot be compiled at this
revision. ``hg bisect`` and ``git bisect`` skip a revision if the command exit
code is 125.

The idea is similar to :ref:`dichotomy <debug-dichotomy>`: reduce the quantity
of code that have to be read to find a bug.


.. _debug-dichotomy:

Dichotomy
---------

Dichotomy or "divide to conquer" ;-)

The idea of the "dichotomy" methodology is to reduce the quantity of executed
code before the bug is triggered. To reduce the quantity of code, you can:

* comment function calls
* disable most features: turn off logging, turn off audio and/or video
  playback, etc.
* comment large partion of code

The goal is not the reduce the code to a single line of code reproducing the
bug. The goal is the reduce the quantity of code that should be read manually
to find the bug.

The debug method can sometimes take several hours, so it's nice to have
"milestones": backup points where the bug can still be reproduced. If you
use a Version Control System (VCS like Git or Mercurial), you can use local
commits (ex: create a local branch in git). Don't worry of the change content
or the commit message, ``plop`` is a great commit message for such changes :-)
These milestones are important to be able to go backward if the bug cannot be
reproduced anymore when you disabled too much code and features.

Add printf
----------

Debuggers are great, convenient and powerful. But. Sometimes, a bug cannot be
reproduce in the debugger for an unknown reason, or the control flow is too
complex to run the application in a debugger. For example, it's hard to debug
an event based application where a single logical "function" (or coroutine) is
splitted into several small callbacks.

In such case, an easy method is to add "print" calls (ex: ``printf()`` in C or
``print`` in Python) in the code to "dump" the control flow, to try to bisect
manually the code. Example of a Python function body::

    func1(a)
    func2(b)
    return func3(c)

Add ``print`` calls to see where the bug is triggered::

    print("func1")
    func1(a)
    print("func2")
    func2(b)
    print("func3")
    res = func3(c)
    print("exit")
    return res

The last instruction was splitted into two instructions to see if the bug
occurs before the call to ``func3()`` or after.

If you see ``func1`` and ``func2`` but not ``func3``, the bug occurred after
the line ``print("func2")`` and before ``print("func3")``, so the bug occurred
on the ``func2()`` call.

You can now remove the ``print("func1")`` line (to have a less verbose output),
and continue to add ``print`` calls inside the ``func2()`` function.  Iterate
until you have a few functions to read to find the bug. It's common to get the
failing line in less than 5 iterations, the technic looks very basic, but it's
fast if the scenario to reproduce the bug is reliable.

Debugging can be painful, so don't hesitate to make it more funny by using
less boring messages than ``func1`` or ``func3`` :-) I'm using:

* ``LA`` (here in french)
* ``1``
* ``1b``
* ``pouet``
* ``@@@@@@@@@@@``
* etc.

.. note::
   If the source code is not tracked by a Version Control System (VCS like Git
   or Mercurial), don't forget to create backup of files to easily remove
   these print calls when the bug is identified.


Gdb
===

* Pretty printer: ``set print pretty on``
* Enter TUI/exit TUI: CTRL+x a
* https://sourceware.org/gdb/onlinedocs/gdb/TUI-Keys.html
* CTRL+x o: change active window
* Display full print value: ``set print elements 1024``
  (or ``set print elements 0`` if you are brave)
* Print variable type: ``whatis variable``
* Dump the structure of a variable: ``ptype variable``
* LD_LIBRARY_PATH: ``gdb -iex "set env LD_LIBRARY_PATH=$PWD" --args ./python Lib/test/gdb_sample.py``
* Autoload Python: ``set auto-load python-scripts on``
* Load a Python script: ``source script.py``


x86_64 assembler, gdb
=====================

https://en.wikipedia.org/wiki/X86_calling_conventions#System_V_AMD64_ABI

Stack aligned on 16 bytes boundary.

Calling convention:

* arg1: RDI
* arg2: RSI
* arg3: RDX
* arg4: RCX
* arg5: R8
* arg6: R9


gdb
===

* Truncated string: ``set print elements 0``

* TUI:

  * CTRL+x a: enable/disable TUI
  * (Inside TUI) CTRL+x o: switch to the next TUI window
  * See also https://sourceware.org/gdb/onlinedocs/gdb/TUI-Keys.html

* Stop on PyType_Ready() but only if type->tp_name is the string "_ModuleLock"::

    (gdb) b PyType_Ready
    Breakpoint 2 at 0x4faa9c: file Objects/typeobject.c, line 4980.

    (gdb) run
    ...
    Breakpoint 2, PyType_Ready (type=0x953ba0 <PyBaseObject_Type>) at Objects/typeobject.c:4980
    4980	    if (type->tp_flags & Py_TPFLAGS_READY) {

    (gdb) condition 2 strcmp(type->tp_name, "_ModuleLock")==0
    (gdb) cont

    Breakpoint 2, PyType_Ready (type=0x9ecf78) at Objects/typeobject.c:4980
    4980	    if (type->tp_flags & Py_TPFLAGS_READY) {
    (gdb) p type->tp_name
    $6 = 0x7ffff7f83080 "_ModuleLock"

* Breakpoint on a value::

    (gdb) watch type->tp_init
    Hardware watchpoint 4: type->tp_init

    (...)

    Hardware watchpoint 4: type->tp_init

    Old value = (initproc) 0x0
    New value = (initproc) 0x4f3e6e <object_init>
    inherit_slots (type=0x9ecf78, base=0x953ba0 <PyBaseObject_Type>) at Objects/typeobject.c:4944


* Run until line 4988::

    (gdb) u	4899
    inherit_slots (type=0x9ecf78, base=0x953ba0 <PyBaseObject_Type>) at Objects/typeobject.c:4899


Write a core dump in disk
=========================

Fedora catchs fatal errors like segmentation faults with its application ABRT.
To develop, sometimes it helps to get a core dump. It's possible to write
a core dump on disk with::

    ulimit -c unlimited
    sudo bash -c "echo '%e-%p.core' > /proc/sys/kernel/core_pattern"

Test::

    $ python3
    >>> import faulthandler; faulthandler._sigsegv()
    Erreur de segmentation (core dumped)
    $ ls *core*
    python3-27542.core


Display a wchar_t string
========================

Use this macro::

    define wc_print
    echo "
    set $c = (wchar_t*)$arg0
    while ( *$c )
      if ( *$c > 0x7f )
        printf "[%x]", *$c
      else
        printf "%c", *$c
      end
      set $c++
    end
    echo "\n
    end


Breakpoint in GDB
=================

Write following code into ``bp.py``::

    class MyBreakpoint(gdb.Breakpoint):
        def stop(self):
            caller = gdb.newest_frame().older()
            caller_name = caller.name() if caller else 'none'
            return (caller_name != 'func_dealloc')

    MyBreakpoint('func_clear')

In gdb, type: ``source bp.py``.

It puts a breakpoint on the function ``func_clear()`` but stop if the
the caller function name is not ``func_dealloc()``.


Reverse
=======

* http://www.sourceware.org/gdb/wiki/ProcessRecord/Tutorial
* "Process record does not support instruction 0xc5 at address ...":
  gdb doesn't support AVX. Workaround?

  * LD_HWCAP_MASK=0?
