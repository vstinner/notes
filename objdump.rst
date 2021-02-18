++++++++++++++++++++++++++
objdump: inspect ELF files
++++++++++++++++++++++++++

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

