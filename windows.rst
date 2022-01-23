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

=======================  =========================  ==========================================================
Windows command          UNIX command               Comment
=======================  =========================  ==========================================================
``set``                  ``env``                    Display all environment variables
``type file.exe``        ``cat file.txt``           Display the content of ``file.txt``
``echo %PATH%``          ``echo $PATH``             Display the value of the ``PATH`` environment variable
``RMDIR /S /Q dir``      ``rm -rf dir``             Remove a directory and its content
``cmd > log``            ``cmd > log``              Redirect command stdout into a new ``log`` file
``cmd >log 2>&1``        ``cmd >log 2>&1``          Redirect command stdout and stderr into a new ``log`` file
``cmd >NUL``             ``cmd >/dev/null``         Ignore command stdout (redirect it to null)
``echo %errorlevel%``    ``echo $?``                Display the exit code of the previous command
``set PROMPT=$$ ``       ``export PS1='$ '``        Change the command line prompt to ``$ ``
``dir NAME /s /p``       ``find -name NAME``        Find a file by its name in subdirectories
``shutdown /p /f``       ``sudo poweroff``          Turn off the computer
``findstr PATTERN *.c``  ``grep PATTERN *.c``       Search *PATTERN* in files with name ending with ``.c``
``cd``                   ``pwd``                    Current directory
=======================  =========================  ==========================================================

Get usage::

    findstr /?

grep in subdirectories::

    findstr /S PATTERN *.c

To emulate top on Windows, run powershell.exe and type::

    while (1) { ps | sort -desc cpu | select -first 15; sleep -seconds 2; cls }

Press CTRL+c to stop it.


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
variant) and use a "Pro - Retail" product key. Create of a VM with 60 GB of
disk (prevously I used 40 GB, it was too small).

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
* 996: ERROR_IO_INCOMPLETE: Overlapped I/O event is not in a signaled state.
* 10060: WSAETIMEDOUT

See the full list of `Windows System Error Codes
<https://docs.microsoft.com/en-us/windows/desktop/debug/system-error-codes>`_.


Windows exceptions
==================

* EXCEPTION_ACCESS_VIOLATION = STATUS_ACCESS_VIOLATION = ``c0000005`` (hex) = ``3221225477`` or ``-1073741819``
* CONTROL_C_EXIT = STATUS_CONTROL_C_EXIT = ``C000013A`` (hex) = ``3221225786``
* STATUS_STACK_BUFFER_OVERRUN = ``C0000409`` (hex) = ``3221226505``
* https://github.com/wine-mirror/wine/blob/master/include/winbase.h
* https://github.com/wine-mirror/wine/blob/master/include/winnt.h


OpenSSH server
==============

Copy your SSH key
-----------------

Open ``C:\Users\vstinner\.ssh\authorized_keys`` file and put your public key
there. Then fix file permissions::

    icacls.exe "C:\Users\vstinner\.ssh\authorized_keys" /inheritance:r /grant "Administrators:F" /grant "SYSTEM:F"

If your user is an administrator, you should edit the file ``C:\ProgramData\ssh\administrators_authorized_keys`` instead.
Again, you need to change the permissions::

    icacls.exe "C:\ProgramData\ssh\administrators_authorized_keys" /inheritance:r /grant "Administrators:F" /grant "SYSTEM:F"

Documentation: `OpenSSH key management <https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_keymanagement>`_.

Enable sshd server logs
-----------------------

* As an administrator, edit ``C:\ProgramData\ssh\sshd_config``
* Add ``SyslogFacility LOCAL0``.
* Restart the sshd server: ``net stop sshd`` and then ``net start sshd``
  (type these commands in an administrator terminal).

Enable sshd server
------------------

* Go to Settings
* Search for "Manage Optional Features"
* Add an optional feature: "OpenSSH Server"
* Install it.
* Go to the Windows Start menu, search for Services.
* In Services, search for the OpenSSH SSH Server.
* Right click, properties:

  * Starting type: Automatic.
  * Click: OK

* Right click: Start.

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


Disable Windows Defender Realtime protection
============================================

On an idle Windows VM, the VM uses between more than 150% of the CPU. If I move
the mouse cursor, the CPU usage goes to 50%. It is the ``msmpeng.exe`` process
which uses the CPU. "ps" in PowerShell and the Task Manager don't agree
on the CPU usage: 50% according to ps, 2% according to the Task Manager...

If I disable Real Time protection in Windows Defender, the feature is enabled
again at next reboot...

I had to add a key into registry to ensure that Windows doesn't reenable
Real Time protection after reboot:

* run regedit.exe
* Go to HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Defender
* Create a "DWORD (32-bit)" key called "DisableAntiSpyware", set its value
  to 1.
* Done.


Maximum path length
===================

* https://docs.microsoft.com/en-us/windows/win32/fileio/naming-a-file
* MAX_PATH = 260 characters
* Does the **system** support long path? Query ``ntdll.RtlAreLongPathsEnabled()``

Application manifest to opt-in for "long path"::

    <application xmlns="urn:schemas-microsoft-com:asm.v3">
      <windowsSettings>
        <longPathAware xmlns="http://schemas.microsoft.com/SMI/2016/WindowsSettings">true</longPathAware>
      </windowsSettings>
    </application>

An application only supports long if the system supports long path and the
application opts in for long path.

C languages: Windows types
==========================

`Windows Data Types
<https://docs.microsoft.com/en-us/windows/win32/winprog/windows-data-types>`_:

* ``LPCTSTR``: ``CONST WCHAR *`` if ``UNICODE`` defined, ``CONST CHAR *``
  otherwise
* ``UINT:``: ``unsigned int``

C Runtime library (CRT)
=======================

Visual Studio provides a C Runtime library (CRT). Its source code can be found
in: "%ProgramFiles(x86)%\Windows Kits\10\Source\10.0.[version]\ucrt\env".

Debug Windows Update failure
============================

* Google the error code
* Open cmd.exe as an adminitrator and run: ``sfc /scannow``
  (SFC fixes system files integrity)
* Open cmd.exe as an adminitrator and run:
  ``DISM /Online /Cleanup-Image /RestoreHealth``
  (repair corrupted files of installed packages)

Not tested: ``CHKDSK C: /F /R`` (``/F`` repairs errors, ``/R`` checks for bad
sectors).


MSDN
====

* Download Windows 10 ISO: https://www.microsoft.com/en-us/software-download/windows10ISO
* Get a Windows Product key: https://my.visualstudio.com/productkeys

Time
====

Kernel ticks:

* The kernel uses an interruption at 64 Hz: 15.625 ms per **tick**
* NtQueryTimerResolution() gives the min/max and current resolution of the tick

Wait:

* WaitForSingleObject(): resolution of **1 tick**
* Sleep(): resolution of **1 tick**

System clock:

* GetSystemTimeAsFileTime(): resolution of **1 tick**
* GetSystemTimePreciseAsFileTime() (Windows 8 and newer)

Monotonic clock:

* GetTickCount64(): resolution of **1 tick**

Performance counter:

* QueryPerformanceCounter(): resolution of 1 / frequency (100 ns on Windows 10)
* QueryPerformanceFrequency(): 10 MHz on Windows 10

Timer:

* CreateWaitableTimer()
* SetWaitableTimer(): resolution of 100 ns

Multimedia API, ``winmm.lib`` and ``timeapi.h``:

* Frequency up to 1 kHz: 1 ms per tick
* timeBeginPeriod()

  * "Setting a higher resolution can improve the accuracy of time-out intervals
    in wait functions. However, it can also reduce overall system performance,
    because the thread scheduler switches tasks more often. High resolutions
    can also prevent the CPU power management system from entering power-saving
    modes. Setting a higher resolution does not improve the accuracy of the
    high-resolution performance counter."

See also:

* `The Windows Timestamp Project <http://www.windowstimestamp.com/description>`_
