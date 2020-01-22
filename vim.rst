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
