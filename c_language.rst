++++++++++++++++++++++
C programming language
++++++++++++++++++++++

See also:

* :ref:`GDB <gdb>`
* :ref:`Visual Studio <visual-studio>`

Lack of namespaces
==================

* Common prefix for identifiers to prevent conflicts:

  * glib: ``g_``
  * Gtk: ``gtk_``
  * Python: ``Py_``, ``_Py_`` ("private") or ``PY_`` (define)

* ``static`` keyword

  * function only accessible from the current file, not exported
  * variable only accessible from the current file, not exported
  * variable local to a function

* ``#include``: C preprocessor

Python has the ``make smelly`` tool to detect exported symbols which doesn't
start with ``Py_`` nor ``_Py_``.


Issues with types
=================

* comparison between signed and unsigned: who wins? cast signed to unsigned,
  or cast unsigned to signed? => obvious integer overflow
* integer overflow: undefined behaviour, the compiler is free to optimize.
  Check if an operation will overflow is hard, **especially** for signed
  numbers. GCC added builtin functions to check that in a portable and
  efficient way.
* portability: int==long==void*, no warning. if int and long have the same
  size, downcasting a long into an int is allowed, and don't emit any warning.
* int stored in void*
* void* vs intptr_t vs uintptr_t
* Use "int" to access an item of an array in a loop: the compiler may
  have to handle integer overflow. size_t or ssize_t preferred here?


Portability
===========

* Perl still uses C89
* Python only started to move to C99 with Python 3.6, only CPython is
  restricted to a **subset** of C99, the most portable parts of C99...
* GNU extensions of GCC
* glibc vs all other C libraries (ex: musl libc and uclibc). GNU extensions,
  again. Implementation bugs. Errno is sometimes set to 0 on success, sometimes
  it is not set on failure, it depends on the called function and the libc.
* ``<stdint.h>`` not fully supported in 2017, need some hacks to support old C
  compilers
* ``<stdatomic.h>`` is still "new" and not well supported by C compilers
* ``<stdbool.h>``?


Issues with C++
===============

* C code used in C++ has to be careful with exceptions: need to compile C with
  ``-fexceptions``?
* ``extern {`` trickery for header files


Undefined Behaviour
===================

* `What Every C Programmer Should Know About Undefined Behavior #1/3
  <http://blog.llvm.org/2011/05/what-every-c-programmer-should-know.html>`_
* `What Every C Programmer Should Know About Undefined Behavior #2/3
  <http://blog.llvm.org/2011/05/what-every-c-programmer-should-know_14.html>`_
* `What Every C Programmer Should Know About Undefined Behavior #3/3
  <http://blog.llvm.org/2011/05/what-every-c-programmer-should-know_21.html>`_
* GCC Undefined Behavior Sanitizer, ``ubsan``: ``-fsanitize=undefined``
* `Clang UndefinedBehaviorSanitizer
  <https://clang.llvm.org/docs/UndefinedBehaviorSanitizer.html>`_


Strict Aliasing
===============

* `Understanding Strict Aliasing
  <http://cellperformance.beyond3d.com/articles/2006/06/understanding-strict-aliasing.html>`_ (Mike Acton, June 1, 2006)
* `Demystifying The Restrict Keyword
  <http://cellperformance.beyond3d.com/articles/2006/05/demystifying-the-restrict-keyword.html>`_ (Mike Acton, May 29, 2006)


C aliasing
==========

* ``-fstrict-aliasing`` vs ``-fno-strict-aliasing``
* ``__restrict__`` (or just ``restrict``)
* clang "bug": `aliasing bug with union in clang 4.0
  <https://bugs.llvm.org//show_bug.cgi?id=31928>`_
* `Understanding Strict Aliasing
  <http://cellperformance.beyond3d.com/articles/2006/06/understanding-strict-aliasing.html>`_
  (Mike Acton, June 1, 2006)
* `Demystifying The Restrict Keyword
  <http://cellperformance.beyond3d.com/articles/2006/05/demystifying-the-restrict-keyword.html>`_
  (Mike Acton, May 29, 2006)
* `Type-punning and strict-aliasing
  <http://blog.qt.io/blog/2011/06/10/type-punning-and-strict-aliasing/>`_
  (Thiago Macieira, June 2011)
* Python 2 slower: the C code base doesn't respect strict aliasing and so must
  be compiled with ``-fno-strict-aliasing`` (to avoid bugs when the compiler
  optimizes the code) which is inefficient. The structure of Python C type has
  been deeply rewritten to fix the root cause.
* `gcc-help: Missed optimization when using a structure
  <https://gcc.gnu.org/ml/gcc-help/2013-04/msg00192.html>`_ (2013-04)
* `GCC -fstrict-aliasing documentation
  <https://gcc.gnu.org/onlinedocs/gcc/Optimize-Options.html#Type-punning>`_
* `GCC Union documentation
  <https://gcc.gnu.org/onlinedocs/gcc/Structures-unions-enumerations-and-bit-fields-implementation.html#Structures-unions-enumerations-and-bit-fields-implementation>`_
* `Detecting Strict Aliasing Violations
  <http://trust-in-soft.com/wp-content/uploads/2017/01/vmcai.pdf>`_
  by P. Cuoq et. al.

Change which fixed a crash after the merged of the new dict implementation
on a specific platform (don't recall which one!):
https://github.com/python/cpython/commit/186122ead26f3ae4c2bc9f6715d2a29d339fdc5a

Example::

    #include <stdint.h>
    #include <stdio.h>

    uint32_t
    swap_words( uint32_t arg )
    {
      uint16_t* const volatile sp = (uint16_t*)&arg;
      uint16_t        hi = sp[0];
      uint16_t        lo = sp[1];

      sp[1] = hi;
      sp[0] = lo;

      return (arg);
    }

    int main(void)
    {
        uint32_t x = 0xabcd1234;
        uint32_t y = swap_words(x);
        printf("x=%lx\n", (long unsigned int)x);
        printf("y=%lx\n", (long unsigned int)y);
        return 0;
    }

Bug::

    $ LANG= gcc -O3 x.c -o x -fstrict-aliasing -Wstrict-aliasing=2 && ./x
    x.c: In function 'swap_words':
    x.c:7:3: warning: dereferencing type-punned pointer will break strict-aliasing rules [-Wstrict-aliasing]
       uint16_t* const volatile sp = (uint16_t*)&arg;
       ^~~~~~~~
    x=abcd1234
    y=abcd1234


volatile
========

volatile is discouraged in the Linux kernel in favor of smaller locks:
https://github.com/torvalds/linux/blob/master/Documentation/process/volatile-considered-harmful.rst


GCC warnings
============

* ``-Wall``: some warnings
* ``-Wall -Wextra``: more warnings
* ``-Wall -Wextra -O3``: even more warnings. Some warnings are only emitted
  when the compiler optimizes the code, like dead code or unused variables.
* There are even more. GCC is able to emit even more warnings, but they must
  be enabled explictly!

  * ``-fstrict-aliasing -Wstrict-aliasing=2``


Platforms #define
=================

* AIX: ``#ifdef _AIX``
* FreeBSD: ``#ifdef __FreeBSD__``
* Linux: ``#ifdef __linux__``
* NetBSD: ``#ifdef __NetBSD__``
* Solaris: ``#ifdef sun``
* Windows: ``_WIN32`` or ``_WIN64``
* macOS: ``#ifdef __APPLE__``


Compiler defines
================

* `GCC <https://gcc.gnu.org/>`_:
  ``#if defined(__GNUC__) && ((__GNUC__ > 4) || ((__GNUC__ == 4) && (__GNUC_MINOR__ > 5)))``
* `Clang <https://clang.llvm.org/>`_:
  ``#ifdef __clang__``
* :ref:`Visual Studio <visual-studio>`:
  ``#if defined(_MSC_VER) && _MSC_VER >= 1800``


GCC flags
=========

https://developers.redhat.com/blog/2018/03/21/compiler-and-linker-flags-gcc/
