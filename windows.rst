.. _windows:

++++++++++++++++++++++++++++++++++++
Survivor Guide to Develop on Windows
++++++++++++++++++++++++++++++++++++

Guide written for Linux developers.

Useful tools
============

* `ConEmu <https://conemu.github.io/>`_
* `Firefox <http://www.mozilla.com/fr/firefox/>`_
* `7-zip <http://www.7-zip.org/>`_: archive manager (.zip, .tar.gz, .7z, .rar, etc.)
* `Gvim <http://www.vim.org/download.php#pc>`_: text editor gvim (Gtk+ version for Windows)
* `Python <http://www.python.org/>`_
* `MSYS <http://www.mingw.org/wiki/MSYS>`_: terminal using bash for Windows
* `WinSCP <http://winscp.net/>`_: secury file copy on the network (SSH protocl)
* `tortoisehg <http://tortoisehg.bitbucket.org/>`_


Windows console
===============

* Kill a blocked command (harder than CTRL+c): CTRL + Scroll Lock key. (send a
  ``SIGBREAK`` signal)

Note: On my Lenovo T430 laptop, I have to use the "Fn" key:

* Fn + B: Break
* Fn + P: Pause
* Fn + S: SysRq

Alternative terminals for Windows:

* `ConEmu <https://conemu.github.io/>`_
* `mintty <https://mintty.github.io>`_


cmd.exe (Windows "shell", Windows console, the MS-DOS black window)
===================================================================

* Change prompt: ``set PROMPT=$P$G``

* Redirect stdout and stderr into the file ``outlog.log``:
  ``command >output.log 2>&1``

======================  ====================  ==========================================================
Windows command         UNIX command          Comment
======================  ====================  ==========================================================
``set``                 ``env``               Display all environment variables
``type file.exe``       ``cat file.txt``      Display the content of ``file.txt``
``echo %PATH%``         ``echo $PATH``        Display the value of the ``PATH`` environment variable
``RMDIR /S /Q dir``     ``rm -rf dir``        Remove a directory and its content
``cmd > log``           ``cmd > log``         Redirect command stdout into a new ``log`` file
``cmd >log 2>&1``       ``cmd >log 2>&1``     Redirect command stdout and stderr into a new ``log`` file
``cmd >NUL``            ``cmd >/dev/null``    Ignore command stdout (redirect it to null)
``echo %errorlevel%``   ``echo $?``           Display the exit code of the previous command
``set PROMPT=$$ ``      ``export PS1='$ '``   Change the command line prompt to ``$ ``
======================  ====================  ==========================================================


Configure vim on Windows
========================

* Right click on gvim: Run as administrator
* Open /program files (x86)/vim/_vimrc
* Comment the lines ``source $VIMRUNTIME/mswin.vim`` and ``behave mswin``
* Add custom config


Mount Windows directory on Linux
================================

Command to mount the Widows "test" directory locally to ``~/mnt``, local
files will be owned by the user ``haypo:haypo``::

    sudo mount.cifs '//192.168.0.14/test' ~/mnt -o 'user=USERNAME,pass=PASSWORD,uid=haypo,gid=haypo'

.. _visual-studio:

Visual Studio
=============

Flavors:

* Express
* Professional: enough to build Python
* Ultimate

Versions:

=============  ======  ========
Visual Studio  MSVC++  _MSC_VER
=============  ======  ========
         2017    14.1      1910
         2015    14.0      1900
         2013    12.0      1800
         2012    11.0      1700
         2010    10.0      1600
         2008     9.0      1500
         2005     8.0      1400
         2003     7.1      1310
         ---      7.0      1300
         ---      6.0      1200
         ---      5.0      1100
=============  ======  ========

Configure a shell to use the VS C compiler in 64-bit mode::

    "%VS140COMNTOOLS%\..\..\VC"\vcvarsall.bat amd64

Argument:

* ``x86``: compile in 32-bit mode
* ``amd64``: compile in 64-bit mode
* ``x86_amd64``: cross-compile to 64-bit mode on a 32-bit system


Configuration
=============

Git configuration file
----------------------

Filename: ``C:\Users\haypo\.gitconfig``. Run cmd.exe as administrator to be
allowed to create symbolic links.

Windows console, cmd.exe
------------------------

Right click on the title, Properties: set Buffer Size of Command History to
999 (default: 50).

See also
========

* :ref:`Operating systems <operating-systems>`

Windows variants
================

To develop on CPython: get a "multi-version" of Windows 10 (no N, KN or VL
variant) and use a "Pro - Retail" product key. Create of a VM with 40 GB of
disk.

Flavors:

* Family: basic feature set
* Pro: more features
* Entreprise: even more features

Variants:

* "N": Not with Media Player; for Europe.
* "KN": specially designed for Korean market and does not include Windows Media
  Player (WMP) and an instant messenger.
* "VL": Volume License,  a single license key can be used to activate multiple
  installations of Windows 10. This is usually used by large enterprises.
* "S": "Windows 10 S can only run apps from the Windows Store". Windows 10 S is
  designed to run well even on lower-end laptops. Windows 10 S is focused on
  speed, better battery life, and higher performance.


Some Windows error codes
========================

* 5: ERROR_ACCESS_DENIED: Access is denied.
* Exception Code: ``c0000005`` (decimal: ``3221225477`` or ``-1073741819``):
  "access violation", EXCEPTION_ACCESS_VIOLATION.
* 996: ERROR_IO_INCOMPLETE: Overlapped I/O event is not in a signaled state.

See the full list of `Windows System Error Codes
<https://docs.microsoft.com/en-us/windows/desktop/debug/system-error-codes>`_.


OpenSSH server
==============

To use the OpenSSH server from Microsoft (the "Optional feature"), you need
at least Windows 10 build 1803. Before, this flavor was unusable.

* Go to settings, search for "Manage Optional Features": enable OpenSSH
* In my case, I had to run ``\Windows\System32\OpenSSH\ssh-keygen -A``
* The SSH private key is stored in ``%ProgramData%\ssh\ssh_host_ed25519_key``.
  This file must be owned by SYSTEM and the only permission must be that SYSTEM
  is allowed to Read this file.
* To allow incoming TCP connections to port 22 (SSH), run PowerShell as administrator and type::

    New-NetFirewallRule -Name sshd -DisplayName 'OpenSSH SSH Server' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22

* Copy your SSH public key into ``C:\Users\vstinner\.ssh\authorized_keys`` (replace
  vstinner with your username!)
* Go to Windows Menu>search for "Services". In Services, search for "OpenSSH
  Server": click on Start.
* If OpenSSH server doesn't work, look into ``%ProgramData%\ssh\Logs\sshd.log``
* If the server works, you can change the Service start from Manual to
  Automatic.

To debug, you can install psexec, open a shell as SYSTEM with
``psexec -i -s -d cmd.exe`` and then type:
``C:\Windows\System32\OpenSSH\sshd.exe`` to run the SSH server in foreground.

Files and directories:

* ``C:\Windows\System32\OpenSSH\sshd.exe``: the SSH server program
* ``C:\ProgramData\ssh\ssh_host_ed25519_key``: SSH server private key
* ``C:\ProgramData\ssh\sshd_config``: SSH server configuration file
* ``C:\ProgramData\ssh\Logs\sshd.log``: SSH server logs

Misc
====

* Get system load:: ``wmic cpu get loadpercentage``
