++++++++++++++++++++++++++++++++
Fragmentation of the Heap Memory
++++++++++++++++++++++++++++++++

* http://python.dzone.com/articles/diagnosing-memory-leaks-python
* http://bugs.python.org/issue11849
* high fragmentation of the memory heap on Windows
  http://bugs.python.org/issue19246
* http://bmaurer.blogspot.it/2006/03/memory-usage-with-smaps.html
* https://mail.gnome.org/archives/gnome-list/1999-September/msg00036.html
* http://www.canonware.com/jemalloc/
* When Linux Runs Out of Memory, by Mulyadi Santosa (11/30/2006)
  http://www.linuxdevcenter.com/pub/a/linux/2006/11/30/linux-out-of-memory.html?page=1
* glibc: 3 Virtual Memory Allocation And Paging
  http://www.gnu.org/software/libc/manual/html_node/Memory.html#Memory
* malloc_trim()
* malopt():

  * M_TRIM_THRESHOLD: default=256** 1024
  * M_MMAP_THRESHOLD: default=256** 1024
  * M_MMAP_MAX: default=65536

* GNU libc

  * glibc doc: Efficiency Considerations for malloc
    http://www.gnu.org/software/libc/manual/html_mono/libc.html#Efficiency-and-Malloc
  * mmap thredshold: 256 KB by default with the GNU libc
  * implementation: ptmalloc

* uClibc

  * implementation: dlmalloc, written by Doug Lea
  * uClibc config: MALLOC_STANDARD=y MALLOC_GLIBC_COMPAT=y
  * malloc for small allocations, while using mmap: the i386 implementation is
    different, see Reorganizing the address space
    http://lwn.net/Articles/91829/

