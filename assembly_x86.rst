++++++++++++++++++
Assembly Intel x86
++++++++++++++++++

Instructions
============

* CDQE: RAX ← sign-extend of EAX.
* MOVSXD rcx,ecx: Move doubleword to quadword with sign-extension.

x86-64 ABI
==========

`System V AMD64 ABI
<https://en.wikipedia.org/wiki/X86_calling_conventions#System_V_AMD64_ABI>`_ (Linux):

* First 6 arguments placed onto registers: RDI, RSI, RDX, RCX, R8, R9.

`Microsoft x64 calling convention
<https://en.wikipedia.org/wiki/X86_calling_conventions#Microsoft_x64_calling_convention>`_:

* First 4 arguments placed onto registers: RCX, RDX, R8, R9.
