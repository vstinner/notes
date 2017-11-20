++++
Time
++++

.. image:: time.jpg
   :alt: Bell tower of a church, Allauch (France)
   :align: right
   :target: http://www.flickr.com/photos/haypo/6100425759/

I wrote the `Python PEP 418 <http://legacy.python.org/dev/peps/pep-0418/>`_
and I added new functions to Python 3.3:

* time.monotonic(): timeout and scheduling, not affected by system clock updates
* time.perf_counter(): benchmarking, most precise clock for short period
* time.process_time(): profiling, CPU time of the process

On Linux older than 2.6.28, select(), poll() and epoll() use kernel jiffies and
so a resolution of ``1/HZ``. HZ can be ready from sysconfig(_SC_CLK_TCK),
``os.sysconfig('SC_CLK_TCK')`` in Python.

Linux 2.6.28:

* `High- (but not too high-) resolution timeouts
  <http://lwn.net/Articles/296578/>`_
* `What's in hrtimer.git for 2.6.28
  <https://lkml.org/lkml/2008/9/20/136>`_
* prctl(PR_GET_TIMERSLACK): 50 us my default. Python module to get/set the
  timer slack: `prctl.get_timerslack(value)
  <https://pythonhosted.org/python-prctl/#prctl.get_timerslack>`_

Windows:

* libvirt: if HPET is present in the XML file of the Virtual Machine::

    <clock offset='localtime'>
        <timer name='hpet' present='yes'/>
    </clock>

* Enable HPET:

  - open a console in adminstrator mode
  - type ``bcdedit /set useplatformclock true``
  - reboot

* Disable HPET:

  - open a console in adminstrator mode
  - type ``bcdedit /deletevalue useplatformclock``
  - reboot

* HPET enabled:

  - time.time() incremented by 15.6 ms,
  - time.monotonic() incremented by 15.0 or 16.0 ms,
  - time.process_time() incremented by 15.6 ms (but unrelated to system time,
    it's the CPU usage time),
  - time.perf_counter() is always incremented (less than 0.2 ms)
  - time.get_clock_info('perf_counter').resolution: 10 ns (1.0e-08) => 100 MHz
  - HPET frequency should be 14.3 MHz

* HPET disabled:

  - xxx

* HPET device missing (ex: disabled in the BIOS):

  - time.time() incremented by 15.6 ms,
  - time.monotonic() incremented by 15.0 or 16.0 ms,
  - time.get_clock_info('perf_counter').resolution: 279.4 ns (2.79e-7) =>
    3.579 MHz (ACPI Power Management Timer)

* Control Panel, périphériques:

  - Compteur d'événements de haute précision => HPET
  - Horloge système CMOS/temps réel

asyncio timeout rounding:

* http://code.google.com/p/tulip/issues/detail?id=106
* http://bugs.python.org/issue20311
* http://bugs.python.org/issue20452
* http://bugs.python.org/issue20505

Other:

* http://www.windowstimestamp.com/
* http://www.haypocalc.com/wiki/Temps

