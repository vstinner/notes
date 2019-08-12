.. _benchmark:

++++++++++
Benchmarks
++++++++++

My articles
===========

* `My journey to stable benchmark, part 1 (system)
  <https://vstinner.github.io/journey-to-stable-benchmark-system.html>`_ (May 21, 2016)
* `My journey to stable benchmark, part 2 (deadcode)
  <https://vstinner.github.io/journey-to-stable-benchmark-deadcode.html>`_ (May 22, 2016)
* `My journey to stable benchmark, part 3 (average)
  <https://vstinner.github.io/journey-to-stable-benchmark-average.html>`_ (May 23, 2016)
* `Visualize the system noise using perf and CPU isolation
  <https://vstinner.github.io/perf-visualize-system-noise-with-cpu-isolation.html>`_ (June 16, 2016)
* `Intel CPUs: P-state, C-state, Turbo Boost, CPU frequency, etc.
  <https://vstinner.github.io/intel-cpus.html>`_ (July 15, 2016)
* `Intel CPUs (part 2): Turbo Boost, temperature, frequency and Pstate C0 bug
  <https://vstinner.github.io/intel-cpus-part2.html>`_
  (September 23, 2016)
* `Analysis of a Python performance issue
  <https://vstinner.github.io/analysis-python-performance-issue.html>`_
  (November 19, 2016)


Factors impacting benchmarks
============================

Factors impacting Python benchmarks:

* Linux Address Space Layout Randomization (ASRL),
  /proc/sys/kernel/randomize_va_space:

  * 0: No randomization
  * 1: Conservative randomization
  * 2: Full randomization

* Python random hash function: PYTHONHASHSEED
* Command line arguments and environmnet variables: enabling ASLR helps here (?)
* CPU power saving and performance features: disable Intel Turbo Boost and/or
  use a fixed CPU frequency.
* Temperature: temperature has a limited impact on benchmarks. If the CPU is
  below 95°C, Intel CPUs still run at full speed. With a correct cooling
  system, temperature is not an issue.
* Linux perf probes: /proc/sys/kernel/perf_event_max_sample_rate
* Code locality, CPU L1 instruction cache (L1c): Profiled Guided Optimization
  (PGO) helps here
* Other processes and the kernel, CPU isolation (CPU pinning) helps here:
  use isolcpus=cpu_list and rcu_nocbs=cpu_list on the Linux kernel command line
* ... Reboot? Sadly, other unknown factors may still impact benchmarks.
  Sometimes, it helps to reboot to restore standard performances.

Commands to check these factors:

* ``python3 -m perf system show`` to show the system state
* ``python3 -m perf system tune`` tunes the system to run benchmarks


Links
=====

* `Biased Benchmarks
  <http://matthewrocklin.com/blog/work/2017/03/09/biased-benchmarks>`_
  (honesty is hard)
* `How to get consistent results when benchmarking on Linux?
  <https://easyperf.net/blog/2019/08/02/Perf-measurement-environment-on-Linux>`_
  (Aug 2019) by Denis Bakhvalov
* `Numbers Everyone Should Know
  <https://everythingisdata.wordpress.com/2009/10/17/numbers-everyone-should-know/>`_
  (2009)
* `How long does it take to make a context switch?
  <http://blog.tsunanet.net/2010/11/how-long-does-it-take-to-make-context.html>`_
  (2010)
* `Rethinking optimization for size <https://lwn.net/Articles/534735/>`_
  (LWN, 2013)
* `Intel Languages Performance <http://languagesperformance.intel.com/>`_


Python resources
================

* `speed@python.org mailing list
  <https://mail.python.org/mailman/listinfo/speed>`_. My threads:

  * `External sources of noise changing call_simple "performance"
    <https://mail.python.org/pipermail/speed/2016-May/000350.html>`_
  * `CPU speed of one core changes for unknown reason
    <https://mail.python.org/pipermail/speed/2016-May/000349.html>`_
  * `When CPython performance depends on dead code...
    <https://mail.python.org/pipermail/speed/2016-April/000341.html>`_
  * `Disable hash randomization to get reliable benchmarks
    <https://mail.python.org/pipermail/speed/2016-April/000329.html>`_
  * `Linux tip: use isolcpus to have (more) reliable benchmark
    <https://mail.python.org/pipermail/speed/2016-February/000276.html>`_
  * `Tool to run Python microbenchmarks
    <https://mail.python.org/pipermail/speed/2016-February/000275.html>`_


Random performance of modern Intel CPU
======================================

https://github.com/cyring/corefreq

Intel CPUs
----------

https://en.wikipedia.org/wiki/List_of_Intel_CPU_microarchitectures

* 2015: Skylake (SKL)
* 2013: Haswell (HSW)
* 2013: Silvermont
* 2011: Sandy Bridge (SNB)
* 2008: Bonnel

  * 2012: Ivy Bridge (IVB)

* 2008: Nehalem (NHM)

  * 2010: Gulftown or Westmere-EP

* 2006: Intel Core


CPU Pipeline
------------

Modern Intel CPUs don't execute CISC machine instructions (complex
instructions) but decode them into RISC instructions (simple instructions).
The RISC instructions are also reordered to reduce the latency of memory load
and store instructions.

Branch prediction
-----------------

The CPU pipeline must decode and reorder instructions faster than the units
executing instructions. To keep the CPU pipeline full, the CPU predicts
branches ("if/else"). If its prediction is wrong, the CPU pipeline must be
flushed and it has a cost on performance.

Linux perf
----------

The Linux perf program gives access to low-level events:

* stalled-cycles-frontend: "The cycles stalled in the front-end are a waste
  because that means that the CPU does not feed the Back End with instructions.
  This can mean that you have misses in the Instruction cache, or complex
  instructions that are not already decoded in the micro-op cache."
* stalled-cycles-backend: "The cycles stalled in the back-end are a waste
  because the CPU has to wait for resources (usually memory) or to finish long
  latency instructions (e.g. transcedentals - sqrt, logs, etc.)."

"Another stall reason is branch prediction miss. That is called bad
speculation. In that case uops are issued but they are discarded because the BP
predicted wrong."

Source: https://stackoverflow.com/questions/22165299/what-are-stalled-cycles-frontend-and-stalled-cycles-backend-in-perf-stat-resul

Memory caches, L1, L2, L3, L4, MMU, TLB
---------------------------------------

Memory accesses are between slow and very slow compared to the speed of the
CPU. To be efficient, there are multiple levels of caches: L1 (fastest, on the
CPU die), L2, L3, and sometimes even L4 (slowest, but also the largest).

Applications don't handle directly physical addresses of the memory but use
"virtual" addresses. The MMU (Memory management unit) is responsible to convert
virtual addresses to physical addresses. When the Linux kernel switches to a
different application, the TLB (Translation lookaside buffer) cache of the MMU
must be flushed.


Micro optimisation
==================

* Linux kernel: `The problem with prefetch
  <https://lwn.net/Articles/444336/>`_: "So the conclusion is: prefetches are
  absolutely toxic, even if the NULL ones are excluded."
* Linux kernel likely() / unlikely() based on GCC __builtin_expect()
* `How new-lines affect the Linux kernel performance
  <https://nadav.amit.zone/linux/2018/10/10/newline.html>`_
  by Nadav Amit


Memory
======

* What Every Programmer Should Know About Memory

  - `HTML version <http://lwn.net/Articles/250967/>`_ (first article which
    ends with links to the following articles)
  - `PDF version
    <http://ftp.linux.org.ua/pub/docs/developer/general/cpumemory.pdf>`_


Help compiler to optimize
=========================

 * const keyword?
 * aliasing: -fno-strict-aliasing or __restrict__


Linux perf
==========

Basic::

    perf stat command

Record::

    perf record -o trace.data -g command
    # -g to record call graph: you may recompile your code with -fno-omit-frame-pointer

Report::

    perf report -i trace.data

Links:

* https://perf.wiki.kernel.org
* http://www.brendangregg.com/perf.html
* http://stackoverflow.com/questions/12601474/what-are-perf-cache-events-meaning
* http://web.eece.maine.edu/~vweaver/projects/perf_events/perf_event_open.html


Valgrind: Callgrind and Cachegrind
==================================

Callgrind
---------

Command::

    PYTHONHASHSEED=0 taskset -c 7 valgrind --dsymutil=yes --tool=callgrind --callgrind-out-file=callgrind.out.slow2.25 --dump-instr=yes --collect-jumps=yes ./slow ../benchmarks/performance/bm_call_simple.py -n 50 --timer perf_counter

* Record at instruction level (not function level)
* Record conditional jumps

Open with Kcachegrind::

    kcachegrind callgrind.out.slow.25.

Or::

    callgrind_annotate callgrind.out.slow.25

.. seealso::
   `Callgrind documentation <http://valgrind.org/docs/manual/cl-manual.html>`_.


Cachegrind
----------

Record traces::

    PYTHONHASHSEED=0 time taskset -c 2 valgrind --dsymutil=yes --tool=cachegrind --cachegrind-out-file=cachegrind.out.fast.25 ./fast ../benchmarks/performance/bm_call_simple.py -n 25 --timer perf_counter

.. seealso::
   `Cachegrind documentation
   <http://valgrind.org/docs/manual/cg-manual.html>`_.
