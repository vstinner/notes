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

