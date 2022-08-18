++++++++++++
Linux kernel
++++++++++++

My kernel bug reports
=====================

* 2022. `Bug 215720 - brk() regression on AArch64 on static-pie binary -- issue with ASLR and a guard page?
  <https://bugzilla.kernel.org/show_bug.cgi?id=215720>`_

  * `Fedora bugreport
    <https://bugzilla.redhat.com/show_bug.cgi?id=2066147>`_

* 2020. `Bug 1797052 - CVE-2020-9391 kernel: brk discards top byte of addresses on aarch64, causing heap corruption in glibc malloc
  <https://bugzilla.redhat.com/show_bug.cgi?id=1797052>`_.
  Initial report by Miro.
  Reported as CVE-2020-9391 security issue.

* 2020. `Bug 1795576 - kernel: VFS and/or XFS filesystem bug with timestamp larger than 32-bit Epoch (year 2038 bug)
  <https://bugzilla.redhat.com/show_bug.cgi?id=1795576>`_, reported by Miro.
  Fixed in XFS of Linux 5.10, need to create a new XFS partition.

* 2016. `Bug 1378529 - intel_pstate driver doesn't support NOHZ_FULL
  <https://bugzilla.redhat.com/show_bug.cgi?id=1378529>`_. Closed as WONTFIX.

ABRT reports
============

* 2020. `Bug 1794350 - [abrt] d_alloc: list_add corruption. next->prev should
  be prev (ffff930b5d4b6ca0), but was 0000000000000000. (next=ffff930beff5b690)
  <https://bugzilla.redhat.com/show_bug.cgi?id=1794350>`_.
  Crash in inotify. Closed as outdated.
* 2020. `Bug 1839782 - nv50_audio_component_get_eld(): general protection fault
  in drm_find_cea_extension() at cold boot
  <https://bugzilla.redhat.com/show_bug.cgi?id=1839782>`_.
  Closed as outdated.
