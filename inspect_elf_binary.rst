++++++++++++++++++++++++++
Inspect an ELF binary file
++++++++++++++++++++++++++

On Linux, they are two main kinds of ELF binary files: programs
(``/usr/bin/bash``) and dynamic libraries (``/usr/lib64/libc.so.6``).

Symbols
=======

List imported symbols::

    objdump -T file

or::

    # -D/--dynamic: display the dynamic symbols rather than the normal symbols
    nm -D file

List exported symbols::

    objdump -T file

Misc
====

Disassemble all sections::

    objdump -d file
