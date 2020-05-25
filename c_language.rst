++++++++++++++++++++++
C programming language
++++++++++++++++++++++

See also:

* :ref:`GDB <gdb>`
* :ref:`Visual Studio <visual-studio>`

i++ and --i
===========

* ``x = ++i;`` is equivalent of ``++i; x = i;`` or ``i += 1; x = i;``
* ``x = i++;`` is equivalent of ``x = i; i++;`` or ``x = i; i += 1;``
* ``x = --i;`` is equivalent of ``--i; x = i;`` or ``i -= 1; x = i;``
* ``x = i--;`` is equivalent of ``x = i; i--;`` or ``x = i; i -= 1;``

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

* ``memcpy(dst, src, 0)`` is safe (if *dst* is a valid address):
  https://stackoverflow.com/questions/29844298/is-it-legal-to-call-memcpy-with-zero-length-on-a-pointer-just-past-the-end-of-an
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
* `Type punning isn't funny: Using pointers to recast in C is bad.
  <https://www.cocoawithlove.com/2008/04/using-pointers-to-recast-in-c-is-bad.html>`_
  (April, 2008) by Matt Gallagher

Magic ``UNION_CAST()`` macro::

   #define UNION_CAST(x, destType) \
      (((union {__typeof__(x) a; destType b;})x).b)


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
* HP-UX: ``#ifdef __hpux``
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


Compile in 32-bit mode on Fedora
================================

* dnf install glibc-devel.i686
* gcc -m32

Example::

    $ echo 'int main() { return sizeof(void *); }' > x.c
    $ gcc x.c -o x -m32 && ./x; echo $?
    4

Configure in 32-bit::

    ./configure CFLAGS="-m32" LDFLAGS="-m32" && make

For Python, install also libffi, openssl and zlib::

    dnf install -y libffi-devel.i686 openssl-devel.i686 zlib-devel.i686

Compiler and linker options
===========================

* https://developers.redhat.com/blog/2018/03/21/compiler-and-linker-flags-gcc/
* https://wiki.debian.org/Hardening

C macros (preprocessor)
=======================

* ``typeof(expr)``: C99
* ``offsetof(type, member)``: ``<stddef.h>``, C89
* ``_builtin_types_compatible_p(type1, type2)``: true if type1 is type2;
  GCC and clang.

Magic ``BUILD_ASSERT_EXPR()`` macro by `Rusty Russell
<http://ccodearchive.net/>`__::

   #define BUILD_ASSERT_EXPR(cond) \
       (sizeof(char [1 - 2*!(cond)]) - 1)

Magic ``ARRAY_LENGTH()`` macro by `Rusty Russell <http://ccodearchive.net/>`__,
compilation error with GCC if the argument is not an array but a pointer::

   #if (defined(__GNUC__) && !defined(__STRICT_ANSI__) && \
       (((__GNUC__ == 3) && (__GNUC_MINOR__ >= 1)) || (__GNUC__ >= 4)))
   /* Two gcc extensions.
      &a[0] degrades to a pointer: a different type from an array */
   #define ARRAY_LENGTH(array) \
       (sizeof(array) / sizeof((array)[0]) \
        + BUILD_ASSERT_EXPR(!__builtin_types_compatible_p(typeof(array), \
                                                          typeof(&(array)[0]))))
   #else
   #define ARRAY_LENGTH(array) \
       (sizeof(array) / sizeof((array)[0]))
   #endif

Is a type signed or unsigned? ::

    #define IS_TYPE_UNSIGNED(type) (((type)0 - 1) > 0)

Libc
----

* ``__GLIBC__``: GNU libc

Convert to a string
-------------------

``STRINGIFY(expr)`` macro::

   #define _XSTRINGIFY(x) #x

   /* Convert the argument to a string. For example, STRINGIFY(123) is replaced
      with "123" by the preprocessor. Defines are also replaced by their value.
      For example STRINGIFY(__LINE__) is replaced by the line number, not
      by "__LINE__". */
   #define STRINGIFY(x) _XSTRINGIFY(x)

``<sys/cdefs.h>`` defines two macros::

   #define __CONCAT(x,y) x ## y
   #define __STRING(x) #x

But ``__CONCAT`` and ``__STRING`` are not portable. For example, NetBSD says
"only works with ANSI C". Comment on Linux: "For these things, GCC
behaves the ANSI way normally, and the non-ANSI way under -traditional."


const
=====

First read: `Why const Doesn't Make C Code Faster
<https://theartofmachinery.com/2019/08/12/c_const_isnt_for_performance.html>`_
(August 2019) by Simon Arneaud.

General:

* ``const int *x`` is the same than ``int const *x``:
  it only matters if ``const`` is before or after ``*``

Single ``*``, constant ``x``, but ``*x`` is mutable::

    int * const x = (int * const)1;
    x = (int * const)2; /* compilation error */
    *x = 3; /* ok */

Single ``*``, constant ``*x``, but ``x`` is mutable::

    const int *x = (const int *)1;
    x = (const int *)2; /* ok */
    *x = 3; /* compilation error */

Single ``*``, constant ``x`` and constant ``*x``::

    const int * const x = (const int * const)1;
    x = (const int * const)2; /* compilation error */
    *x = 3;  /* compilation error */

Problem of casting ``char **`` to ``const char **``:
http://c-faq.com/ansi/constmismatch.html

GCC: use -Wcast-qual option.


Atomic variables
================

* C11 <stdatomic.h>. Supported by:

  * GCC
  * clang

* https://gcc.gnu.org/wiki/Atomic/GCCMM/AtomicSync
* MSC: Interlocked functions like `InterlockedAdd
  <https://docs.microsoft.com/en-us/windows/win32/api/winnt/nf-winnt-interlockedadd>`_.
  Only support 32-bit and 64-bit variables.

Linux kernel: `Detecting and handling split locks
<https://lwn.net/Articles/790464/>`_. Only x86 and x86-64 architectures are
impacted.  Other architectures (such as ARM or RISC-V) do not allow misaligned
memory access. Follow-up: `VMX virtualization runs afoul of split-lock
detection <https://lwn.net/Articles/816918/>`_.

Generic functions:

* ``__atomic_load_n(&var, __ATOMIC_RELAXED)``
* ``__atomic_add_fetch(&var, 1, __ATOMIC_SEQ_CST)``
* ``__atomic_fetch_add(&var, 1, __ATOMIC_SEQ_CST)``
* etc.
* `GCC: Built-in Functions for Memory Model Aware Atomic Operations
  <https://gcc.gnu.org/onlinedocs/gcc/_005f_005fatomic-Builtins.html>`_


C FAQ
=====

http://c-faq.com/
