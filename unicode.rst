+++++++
Unicode
+++++++

.. image:: unicode.png
   :alt: Unicode logo
   :align: right
   :target: http://unicodebook.readthedocs.org/

Read my free ebook: `Programming with Unicode
<http://unicodebook.readthedocs.org/>`_!

Encodings
=========

* Windows

  * OEM code page: used by stdin, stdou and stderr in the Windows console
  * ANSI code page: used by all other Windows "ANSI" functions. Some examples:
    filenames, command line arguments, environment variables, etc.

* UNIX: "Locale encoding"

  * ``LC_CTYPE`` locale
  * used for filenames, command line arguments, environment variables,
    the console (stdin, stdout, stderr)

* Common encodings:

  * UTF-8
  * ISO 8859-1 aka Latin1 or Windows code page 1252
  * ASCII


.. _python-unicode:

Python
======

See my conference (in french) "Comprendre les erreurs Unicode" (Pycon FR 2009
at Paris): `slides (PDF)
<https://github.com/vstinner/conf/blob/master/2009-PyconFR-Paris/comprendre_errurs_unicode.pdf?raw=true>`_
and `video <http://dl.afpy.org/pycon-fr-09/videos/Comprendre_les_erreurs_Unicode.mp4>`_.

Narrow and wide builds, PEP 393
-------------------------------

Python 3.3 introduced the `Flexible String Representation (PEP 393)
<http://www.python.org/dev/peps/pep-0393/>`_ and supports the whole Unicode
range (``U+0000`` - ``U+10ffff``) on all platforms.

Older Python versions had a "narrow or wide" compilation option:

* UNIX and Mac OS X uses wide mode: the ``unicode`` type uses 32-bit code
  points. In Unicode, it is called the ``UCS-4`` encoding.
* Windows uses narrow mode: the ``unicode`` type uses 16-bit code points,
  non-BMP characters (unicode range ``U+10000`` - ``U+10ffff``) are used as
  a surrogate pair (two 16-bit code points). In Unicode, it is called the
  ``UTF-16`` encoding. This mode is preferred on Windows because Windows kernel
  uses also the ``UTF-16`` encoding internally.

Use ``sys.maxunicode == 0xffff`` to check if Python is compiled in narrow mode.
Otherwise, ``sys.maxunicode`` is equal to ``0x10ffff``.


Python 2
--------

* ``str`` type and ``"abc"`` are strings of *bytes*, ``unicode`` type is a
  string of *characters*

* "Default encoding"

  * ``sys.getdefaultencoding()``
  * used by ``unicode.encode()`` and ``str.decode()`` when no encoding is
    specified
  * ASCII by default, must not by modified (``sys.setdefaultencoding()``)

* File system encoding

  * ``sys.getfilesystemencoding()``
  * used to encode filenames and environment variables
  * used on UNIX by ``os.listdir(unicode)`` to decode filenames
  * ANSI code page (``mbcs``) on Windows, ``utf-8`` on Mac OS X, the locale
    encoding on UNIX

* Locale encoding

  * ``locale.getpreferredencoding()``
  * used by default by io.TextIOWrapper
  * ANSI code page on Windows, ``LC_CTYPE`` locale on UNIX

* OEM code page (Windows only)

  * ``sys.stdin.encoding``, ``sys.stdout.encoding`` and ``sys.stderr.encoding``


Python 3
--------

* ``bytes`` type is a string of *bytes*, ``str`` type and ``"abc"`` are strings
  of *characters*

* UTF-8

  * used for the default encoding of the source code

* "Locale encoding"

  * ``locale.getpreferredencoding()``
  * ANSI code page on Windows, ``LC_CTYPE`` locale on UNIX
  * used by ``sys.stdin``, ``sys.stdout``, ``sys.stderr``, and by default by
    ``open()`` (and io.TextIOWrapper)

* "File system encoding"

  * sys.getfilesystemencoding()
  * ANSI code page (``mbcs``) on Windows, ``utf-8`` on Mac OS X, the locale
    encoding on UNIX
  * used for filenames, command line arguments, environment variables

* "Default encoding"

  * ``sys.getdefaultencoding()``, hardcoded to ``utf-8``
  * used by ``bytes.decode()`` and ``str.encode()`` when no encoding is
    specified

* OEM code page (Windows only)

  * ``sys.stdin.encoding``, ``sys.stdout.encoding`` and ``sys.stderr.encoding``


Issues
------

* `GB2312 codec is using a wrong covert table
  <http://bugs.python.org/issue24036>`_: WONTFIX, It's a bug, but one which is
  present in a lot of other systems as well, so we'd potentially make it
  impossible to write GB2312 data which is supposed to be read back by these
  other systems.

