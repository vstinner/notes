++++++++++++++++++++++++++
Multithreading Programming
++++++++++++++++++++++++++

Writing code with threads is hard. Race conditions are likely and common in
multithreaded applications and usually very hard to reproduce.


Threads and Signals
===================

Threads are bad. Threads with signals are worse :-)

Before OpenBSD 5.2, threads were implemented in user space on OpenBSD. Sending
signals was not reliable at all. Before FreeBSD 8, threads+signals had a lot
of issues too.


Spawn Child Processes
=====================

Many tests in test_threading are skipped on FreeBSD <= 6, HP UX11, NetBSD5:

    Between fork() and exec(), only async-safe functions are allowed (issues
    #12316 and #11870), and fork() from a worker thread is known to trigger
    problems with some operating systems (issue #3863): skip problematic tests
    on platforms known to behave badly.


Fork, Exec and File Descriptors
-------------------------------

I wrote `PEP 446 - Make newly created file descriptors non-inheritable
<https://www.python.org/dev/peps/pep-0446/>`_ which breaks backward
compatibility in Python 3.4 "for the good of mankind" (wrote Guido van Rossum).

This PEP makes all file descriptors non-inheritable to fix a race condition:

* two threads create a child process
* thread A creates a pipe
* thread B creates a child process 1
* thread A makes the pipe non-inheritable
* thread A creates a child process 2

Without the PEP, the child process 1 created by the thread B inherit the file
descriptor created by the thread A.

In fact, the race condition is only avoided if the thread A is able to make the
file descriptor non-inheritable atomically, using ``O_CLOEXEC`` or
``SOCK_CLOEXEC`` flag for example.


Python subprocess Module
------------------------

In Python 2, the subprocess module is *not* thread-safe: unexpected file
descriptors can be inherited, and the subprocess has other sily issues.


Process-wide
============

Multithreading is hard because many functions of system C library (libc):

* modify a state for the whole process: change process wide
* is not reentrant
* rely on a global state
* is not "async signal safe"

On Unix and other platforms, many variables are "process-wide", in opposition
of "per thread".

Examples of process-wide states:

* *Current working directory* aka **cwd**

  * Modified by ``chdir()``, read by ``getcwd()``
  * Most "legacy" filesystem functions taking a filename rely on the "current
    working directory" (cwd), especially using relative path. Exampes:
    ``open()`` or ``chmod()``.
  * The new Linux "at" functions don't rely on the current working directory.
    Examples: ``openat()`` or ``chmodat()``.

* Locales

  * Modified by ``setlocale()``
  * For example, used by ``strftime()`` and ``localeconv()``.
  * Functions using "wide character strings" (wcs) avoid some issues.
    Example: ``wcsftime()``.
  * Some libraries don't rely on a global locale but expect a locale argument
  * Recent glibc has a new API to get per-thread locale: XXX

* Unix signals

  * Example of signals: ``SIGINT``, ``SIGSEGV``
  * Signal handlers are registered by ``signal()`` and ``sigaction()``
  * ``raise()`` or ``kill()`` to send a signal to a process
  * Per thread API: ``pthread_kill()`` (send a signal to a thread),
    ``pthread_sigmask()`` (block signals)

* Clock: ``clock_gettime(CLOCK_PROCESS_CPUTIME_ID)``, but there is: CLOCK_THREAD_CPUTIME_ID
* umask: File mode creation mask

  * Get and set by ``umask()``.

Others:

* File descriptors: not really an issue in practice if a FD is only used
  in a single thread.
* Heap memory, malloc()/free(): modern malloc() implementations scales on
  threads/CPUs. Not an issue if a memory block is only used in a single thread.
* User and groups

See also `Ghosts of Unix Past: a historical search for design patterns
<https://lwn.net/Articles/411845/>`_ by Neil Brown (October, 2010).
