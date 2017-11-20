.. _projects:

+++++++++++
My Projects
+++++++++++

Projects of :ref:`Victor Stinner <victor-stinner>`.

.. seealso::
   My :ref:`talks <talks>`, my :ref:`contributions to Free Softwares <contrib>`
   and my :ref:`old projects <old-projects>`.


Websites
========

.. image:: water_lock.jpg
   :alt: Rusty water lock, Camargue (France)
   :align: right
   :target: http://www.flickr.com/photos/haypo/11914396795/

- `Haypo Blog 2 <http://vstinner.github.io/>`_ (new blog, created in 2015)
- `Victor Stinner's Notes <http://vstinner-notes.readthedocs.org/>`_ (this site, created
  in 2014)

Documentation
=============

* `Faster CPython <http://faster-cpython.readthedocs.org/>`_
  (source code: `faster_cpython at github
  <https://github.com/vstinner/faster_cpython>`_)
* `Programming with Unicode <http://unicodebook.readthedocs.org/>`_
  (source code: `unicode_book at github
  <https://github.com/vstinner/unicode_book>`_)
* `CPython Internals <http://cpython-internals.readthedocs.org/>`_
  (source code: `cpython_internals at bitbucket
  <https://bitbucket.org/vstinner/cpython_internals>`_)


Python Projects
===============

.. image:: trollius.jpg
   :alt: Trollius flower, logo of the Trollius project
   :align: right
   :target: http://trollius.readthedocs.org/

* `fatoptimizer <http://fatoptimizer.readthedocs.org/>`_: static optimizer for
  Python 3.6 using function specialization with guards. It is implemented as an
  AST optimizer. It is part of the `FAT Python
  <http://faster-cpython.readthedocs.org/fat_python.html>`_ project.
* `bytecode <http://bytecode.readthedocs.org/>`_: API to modify Python
  bytecode, and a peephole optimizer.
* `faulthandler <http://faulthandler.readthedocs.org/>`_: Dump Python
  tracebacks explicitly, on a fault, after a timeout, or on a user signal.
  The module is part of Python 3.3 and newer.
* `pytracemalloc <http://pytracemalloc.readthedocs.org/>`_: debug tool to
  trace memory blocks allocated by Python. The module is part of Python
  standard library since Python 3.4, I maintain a backport for Python 2.7 and
  3.3 (it should work on Python 2.6-3.3).
* `pyfailmalloc <https://bitbucket.org/vstinner/pyfailmalloc>`_: Debug tool for
  Python injecting memory allocation faults to simulate a low memory system to
  test how your application handles MemoryError exceptions.
* `sixer <https://pypi.python.org/pypi/sixer>`_: add Python 3 support
  to Python 2 applications using the six module.

Other Projects
==============

* `"misc" repository <http://github.com/vstinner/misc>`_:

  - my "dot" files, configuration files: bashrc, hgrc, gitconfig, etc.
  - some command line program: apply_patch.py, scm.py
  - some Python scripts
  - some shell scripts: apt_get.sh, fedora_new_install.sh
