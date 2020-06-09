++++++++++++++++++
Assembly Intel x86
++++++++++++++++++

Instructions
============

* CDQE: RAX ← sign-extend of EAX.
* MOVSXD rcx,ecx: Move doubleword to quadword with sign-extension.
* MOVABS rcx, <imm64>: to load arbitrary 64-bit constant into register and to
  load/store integer register from/to arbitrary constant 64-bit address is
  available.
* ENDBR64: "End Branch 64 bit", Terminate Indirect Branch in 64 bit. Related
  to Control flow Enforcement Technology (CET) hardening
  (-fcf-protection=branch option of GCC). Executed as NOP if the CPU doesn't
  support CET.

Registers
=========

============  ==========  =========  ========
64b register  Lower  32b  Lower 16b  Lower 8b
============  ==========  =========  ========
rax           eax         ax         al
r9            r9d         r9w        r9b
============  ==========  =========  ========

x86-64 ABI
==========

`System V AMD64 ABI
<https://en.wikipedia.org/wiki/X86_calling_conventions#System_V_AMD64_ABI>`_ (Linux):

* First 6 arguments placed onto registers: RDI, RSI, RDX, RCX, R8, R9.

`Microsoft x64 calling convention
<https://en.wikipedia.org/wiki/X86_calling_conventions#Microsoft_x64_calling_convention>`_:

* First 4 arguments placed onto registers: RCX, RDX, R8, R9.
