+++++++++++++++++
vim for developer
+++++++++++++++++

vim command line
================

* ``vim file.c +10``: Open ``file.c`` directly at line 10 (doesn't work with
  ``vi``, only ``vim``)
* ``git diff | vim -``: View the output of a command in vim (``git diff``
  command in this example)

Navigate
========

* ``gg``: go to file start
* ``GG``: go to file end
* ``0``: go to line start
* ``$``: go to line end
* ``:10``: go to line number 10
* ``[[``, ``]]``: jump to previous/next of the class or function
* ``gf``: Go To File, open the file with the file name under the cursor

Buffers
=======

* ``:vs``: Vertical Split
* ``:split``: Horizontal Split
* ``:%bd``: close all buffers

Programming
===========

* Go to a function definition using ctags:

  * Run ":ctags -R" to create an index of symbols (classes, functions, variables)
  * Put the cursor on a symbol: ``CTRL+[`` goes to the symbol defintion

Misc
====

* Open a file from encoding cp850: ``:e ++enc=cp850 document.txt``
* Number of lines of a selection:

  * Create a section
  * Press ``g`` and then ``CTRL+g``.

Windows
=======

* gvim configuration files for user ``vstinner``:

  * ``C:\Users\vstinner\_vimrc``: vim configuration,
    same than ``~/.vimrc`` on Unix
  * ``C:\Users\vstinner\_gvimrc``: gvim configuration,
    same than ``~/.gvimrc`` on Unix

Create a symbol link for configuration files using python::

    C:\Users\vstinner>python
    Python 3.8.0
    >>> import os
    >>> os.symlink(r'\vstinner\misc\conf\vimrc', '_vimrc')
    >>> os.symlink(r'\vstinner\misc\conf\gvimrc', '_gvimrc')

Create a symbol links:

* from ``C:\vstinner\misc\conf\vimrc`` to ``C:\Users\vstinner\_vimrc``
* from ``C:\vstinner\misc\conf\gvimrc`` to ``C:\Users\vstinner\_gvimrc``
