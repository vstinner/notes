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


Test non-ASCII characters with locales
======================================

It seems like FreeBSD 11 doesn't support all encodings: only Latin1 and UTF-8
seem to be implemented.  At least, KOI8-R, Big5 and CP1131 are not implemented
properly.

Windows locales: "fr-FR", "en-US", "ja-JP", etc.

Use cases
---------

* Latin1 or UTF-8 encoding (locale different than C and POSIX)
* C or POSIX locale: ASCII encoding on Linux, Latin1 encoding on
  FreeBSD/Solaris (but ASCII announced by nl_langinfo(CODESET))
* LC_NUMERIC != LC_CTYPE: the fun localeconv() bug, https://bugs.python.org/issue31900
* python 3.7 -X utf8
* macOS and Android UTF-8

Locale, announced encoding, effective encoding
----------------------------------------------

Inconsistent:

================  ==========  ==================  ==================
Operating system  Locale      Announced encoding  Effective encoding
================  ==========  ==================  ==================
FreeBSD           C, POSIX    US-ASCII            ISO-8859-1
FreeBSD           zh_TW.Big5  Big5                ? (not Big5)
macOS             C, POSIX    US-ASCII            ISO-8859-1
macOS             zh_TW.Big5  Big5                ? (not Big5)
================  ==========  ==================  ==================

Consistent, announced encoding = effective encoding:

================  ===========  ==================
Operating system  Locale       Encoding
================  ===========  ==================
Fedora 27         C, POSIX     ASCII
FreeBSD           fr_FR.UTF-8  UTF-8
macOS             fr_FR.UTF-8  UTF-8
Fedora 27         fr_FR.UTF-8  UTF-8
Fedora 27         zh_TW.Big5   Big5
================  ===========  ==================

Tested operating systems:

* macOS 10.13.2:
* FreeBSD 11.1
* Fedora 27 (glibc 2.26)

localeconv()
------------

Fedora 27:

==============  ========  ===============  ========================  ===================================
LC_ALL locale   Encoding  Field            Bytes                     Text
==============  ========  ===============  ========================  ===================================
es_MX.utf8      UTF-8     thousands_sep    ``0xE2 0x80 0x89``        U+2009
fr_FR.UTF-8     UTF-8     currency_symbol  ``0xE2 0x82 0xAC``        U+20AC (€)
ps_AF.utf8      UTF-8     thousands_sep    ``0xD9 0xAC``             U+066C (٬)
uk_UA.koi8u     KOI8-U    currency_symbol  ``0xC7 0xD2 0xCE 0x2E``   U+0433 U+0440 U+043d U+002E (грн.)
uk_UA.koi8u     KOI8-U    thousands_sep    ``0x9A``                  U+00A0
==============  ========  ===============  ========================  ===================================

macOS 10.13.2:

===============  =========  ===============  ========================  ==================================
LC_ALL locale    Encoding   Field            Bytes                     Text
===============  =========  ===============  ========================  ==================================
ru_RU.ISO8859-5  ISO8859-5  currency_symbol  ``b'\xe0\xe3\xd1.'``      U+0440 U+0443 U+0431 U+002e (руб.)
===============  =========  ===============  ========================  ==================================

FreeBSD 11:

===============  =========  ===============  =====================================  =================================================
LC_ALL locale    Encoding   Field            Bytes                                  Text
===============  =========  ===============  =====================================  =================================================
ar_SA.UTF-8      UTF-8      decimal_point    ``b'\xd9\xab'``                        U+066b ('٫')
ar_SA.UTF-8      UTF-8      thousands_sep    ``b'\xd9\xac'``                        U+066c ('٬')
ar_SA.UTF-8      UTF-8      currency_symbol  ``b'\xd8\xb1.\xd8\xb3.\xe2\x80\x8f'``  U+0631 U+002e U+0633 U+002e U+200f ('ر.س.\u200f')
zh_TW.Big5       Big5       currency_symbol  ``b'\xa2\xdc\xa2\xe2\xa2\x43'``        ``u'\uff2e\uff34\uff04'`` (ＮＴ＄)
zh_TW.Big5       Big5       decimal_point    ``b'\xa1\x44'``                        ``u'\uff0e'`` (．)
zh_TW.Big5       Big5       thousands_sep    ``b'\xa1\x41'``                        ``u'\uff0c'`` (，)
===============  =========  ===============  =====================================  =================================================

Note: On FreeBSD with LC_CTYPE="zh_TW.Big5", mbstowcs() doesn't use Big5 but a
different encoding and so returns mojibake.

Windows 7.1:

===============  =========  ===============  ===========  ======
LC_ALL locale    Encoding   Field            Bytes        Text
===============  =========  ===============  ===========  ======
fr-FR            cp1252     currency_symbol  ``b'\x80'``  U+20AC
fr-FR            cp1252     thousands_sep    ``b'\xA0'``  U+00A0
===============  =========  ===============  ===========  ======

strftime(), tzname
------------------

Fedora 27:

==============  ========  ===============  ==============  ===========================
LC_ALL locale   Encoding  Month %b         Bytes           Text
==============  ========  ===============  ==============  ===========================
fr_FR           Latin1    December         ``b'd\xe9c.'``  ``'d\xe9c.'`` (déc.)
==============  ========  ===============  ==============  ===========================

Windows 8.1:

==============  ========  ===============  ==============  ====================
LC_ALL locale   Encoding  Date, format     Bytes           Text
==============  ========  ===============  ==============  ====================
fr-FR           cp1252    December, %b     ``b'd\xe9c.'``  ``'d\xe9c.'`` (déc.)
ja-JP           cp932?    Monday, %a       N/A             ``'\u6708'``
==============  ========  ===============  ==============  ====================

Python2::

    vstinner@apu$ python2
    >>> import time, locale
    >>> locale.setlocale(locale.LC_ALL, "fr_FR")
    'fr_FR'
    >>> time.strftime("%A, %d %B %Y", time.localtime(time.mktime((2018, 2, 1, 12, 0, 0, 0, 0, 0))))
    'jeudi, 01 f\xe9vrier 2018'

* `non-ASCII tzname on Windows <https://bugs.python.org/issue16322#msg173755>`_:
  "'東京 (標準時)' means 'Tokyo (Standard Time)' in Japanese."
* https://bugs.python.org/issue5905
* https://bugs.python.org/issue13560
* https://bugs.python.org/issue16322
* `Commit af02e1c8: Add PyUnicode_DecodeLocaleAndSize() and PyUnicode_DecodeLocale()
  <https://github.com/python/cpython/commit/af02e1c85a66009cdc645a64de7d7ee1335c8301>`_
  "Fix time.strftime() (if wcsftime() is missing): decode strftime() result
  from the current locale encoding, not from the filesystem encoding."
* `Commit 720f34a3:  Issue #5905
  <https://github.com/python/cpython/commit/720f34a3e8567ee7c46ee7d8752617168bfb5258>`_:
  "time.strftime() is now using the locale encoding, instead of UTF-8, if the
  wcsftime() function is not available."

strerror()
----------

===============  ==========  ===========================================  ===========================================
LC_ALL locale    Encoding    Bytes                                        Text
===============  ==========  ===========================================  ===========================================
fr_FR.ISO8859-1  ISO-8859-1  ``b'Fichier ou r\xe9pertoire inexistant'``   ``'Fichier ou r\xe9pertoire inexistant'``
===============  ==========  ===========================================  ===========================================

Links:

* `non-ASCII strerror <https://bugs.python.org/issue13643#msg150031>`_:
  "os.strerror(23) = 'Trop de fichiers ouverts dans le syst\\xe8me'."
* https://bugs.python.org/issue13560
* `Commit 1f33f2b0
  <https://github.com/python/cpython/commit/1f33f2b0c381337d5991c227652d65eadd168209>`_:
  "Issue #13560: os.strerror() now uses the current locale encoding instead
  of UTF-8"


Political and regional differences
==================================

Unicode provides a single standard and so cannot have special cases depending
on country or recent political changes. Examples:

* 2018: `lower() on Turkish letter "İ" returns a 2-chars-long string
  <https://bugs.python.org/issue34723>`_
* 2017: `Germany made the upper case ß official. 'ß'.upper() should now return ẞ.
  <https://bugs.python.org/issue30810>`_

