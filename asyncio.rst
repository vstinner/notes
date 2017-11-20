+++++++++++++++++++++++++++++++++++++++++
The new Python asyncio module aka "tulip"
+++++++++++++++++++++++++++++++++++++++++

Asynchronous becomes very popular nowadays. The Javascript language has
`node.js <http://nodejs.org/>`_, Erlang language has XXX, the Go language has
Goroutines and Channels.  What about Python?

asyncio projects
================

.. image:: trollius.jpg
   :alt: Trollius flower, logo of the Trollius project
   :align: right
   :target: http://trollius.readthedocs.org/

* Python 3.4: `asyncio documentation
  <http://docs.python.org/dev/library/asyncio.html>`_
* Python 3.3: `Tulip project homepage
  <http://code.google.com/p/tulip/>`_
* Python 2.x: `Trollius <https://github.com/vstinner/trollius/>`_



asyncio event loops
===================

* ZeroMQ
* geventreactor
* gevent3
* greenlet
  https://github.com/1st1/greentulip
* libuv: `rose <https://github.com/saghul/rose>`_, a PEP-3156 compatible event
  loop

* Qt:

  - Mark Harviston's PEP 3156 Event-Loop with Qt: https://github.com/harvimt/quamash
  - Twisted qt4reactor: https://github.com/ghtdak/qtreactor/blob/master/qt4reactor.py
  - Twisted qt4reactor: http://bazaar.launchpad.net/~qt4reactor-dev/qt4reactor/trunk/view/head:/qt4reactor.py#L55

* Tk:

  - See Dino Viehland 's talk at Pycon US 2013
  - https://us.pycon.org/2013/schedule/presentation/62/
  - http://www.youtube.com/watch?v=oJQdX_w1vXY

* wxPython: http://twistedmatrix.com/documents/12.3.0/core/howto/choosing-reactor.html#auto13
  and http://wiki.wxpython.org/wxPythonAndTwisted
* Tornado: experimental asyncio support built right into it.
* Glib: `gbulb <https://bitbucket.org/a_ba/gbulb>`_; include Gtk+ and
  GApplication event loops (suitable for GTK+ applications)


Talks about asyncio
===================

* "Tulip: Async I/O for Python 3" by Guido van Rossum, at LinkedIn, Mountain
  View, Jan 23, 2014

  - `Record of a Google Hangout <http://www.youtube.com/watch?v=c7D63mqCs5Y>`_ (2h22)
  - `Slides <https://www.dropbox.com/s/vp7tg8ensbbd4a6/BayPiggies2014.pptx>`_

* "Tulip: Async I/O for Python 3" by Guido van Rossum, Oct 29, 2013 at Twitter
  University for the San Francisco Python User Group

  - `Youtube video <http://www.youtube.com/watch?v=1coLC-MUCJc>`__

* `Tulip or not Tulip <http://fr.slideshare.net/igalarzab/tulip-28638047>`_
  by Jose Ignacio Galarza, Pycon Spain 2013, Nov 26, 2013. Nice introduction to
  Tulip.

* `PEP-3156: Async I/O en Python <http://2013.es.pycon.org/media/asyncio.pdf>`_
  (spanish), by Saúl Ibarra Corretgé, , Pycon Spain 2013, Nov 2013.

* "PyCon 2013 Keynote" by Guido van Rossum, Mar 20, 2013

  - `Youtube video <http://www.youtube.com/watch?v=sOQLVm0-8Yg>`_
  - LWN report: `PyCon: Asynchronous I/O <http://lwn.net/Articles/544522/>`_

* "Python Async IO Horizon" by Lukasz Dobrzanski, Jan 17, 2014

  - `Slides at Slideshare <http://fr.slideshare.net/ssspiochld/python-async-io-horizon>`__

* "A deep dive into PEP-3156 and the new asyncio module" by by Saúl Ibarra
  Corretgé, Feb 03, 2014 (FOSDEM, Bruxelles)

  - `Slides at Slideshare <http://fr.slideshare.net/saghul/asyncio>`__


Tulip projects
==============

* `aiohttp <https://github.com/fafhrd91/aiohttp/>`_:
  HTTP client/server for asyncio (PEP-3156)
* `irc3 <https://github.com/gawel/irc3>`_
  plugable irc client based on python's asyncio
* `rainfall <https://github.com/mind1master/rainfall>`_:
  Here's one more framework =)
  It allows using @asyncio.coroutine for handlers and supports jinja2 templates
* `Vase <https://github.com/vkryachko/Vase>`_


Low-level libraries
===================

What?

* sockets (network), stream (TCP) and datagram (UDP)
* pipes (subprocesses)
* files
* signals

Operating system synchronous I/O multiplexing, I/O event notification facility:

* select
* poll
* epoll: Linux
* kqueue: FreeBSD, Mac OS X, NetBSD, OpenBSD, DragonflyBSD
* devpoll: Solaris
* Windows proactor (IOCP)

C libraries:

* libuv
* libev
* libevent, libevent2

Python libraries:

* pyuv (libuv)
* pyev (libev)
* pyevent (libevent)

Common features:

* asynchronous DNS resolution
* multiplexing


Coroutines
==========

Conference:

* `PyCon 2011: An outsider's look at co-routines
  <http://blip.tv/pycon-us-videos-2009-2010-2011/pycon-2011-an-outsider-s-look-at-co-routines-4899200>`_
  by Peter Portante, Pycon US 2011:

Projects:

* `Toro <https://github.com/ajdavis/toro>`_: Tornado coroutines
* `The difference between yield and yield-from <https://groups.google.com/forum/#!msg/python-tulip/bmphRrryuFk/aB45sEJUomYJ>`_
* `gevent <http://www.gevent.org/>`_:
  coroutine-based Python networking library
* `greenlet <http://greenlet.readthedocs.org/>`_:
  spin-off of Stackless, a version of CPython that supports micro-threads
  called "tasklets"
* `fibers <http://python-fibers.readthedocs.org/en/latest/>`_:
  lightweight concurrent multitasking


High-level libraries
====================

* `gunicorn <http://gunicorn.org/>`_ (sync, eventlet, gevent, tornado): Gunicorn 'Green Unicorn' is a Python WSGI HTTP Server for UNIX
* `diesel <http://diesel.io/>`_
* `uwsgi <http://uwsgi-docs.readthedocs.org/>`_
* `concurrence <https://pypi.python.org/pypi/concurrence>`_
* `Tornado <http://www.tornadoweb.org/>`_:
  web framework and asynchronous networking library, "ideal for long polling,
  WebSockets"
* `Twisted <http://twistedmatrix.com/>`_: event-driven networking engine
* `eventlet <http://eventlet.net/>`_
* ZeroMQ
* `gruvi <https://pypi.python.org/pypi/gruvi>`_
  (`documentation <http://gruvi.readthedocs.org/>`_):
  Synchronous evented IO with pyuv and fibers, based on the
  `PEP 3153: Transport-protocol <http://www.python.org/dev/peps/pep-3153/>`_
* `App Engine NBD
  <http://code.google.com/p/appengine-ndb-experiment/source/browse/ndb/tasklets.py>`_
  by Guido van Rossum
* `obelus <https://pypi.python.org/pypi/obelus/>`_ by Antoine Pitrou: Protocol
  implementation of the Asterisk Manager Interface and Asterisk Gateway
  Interface

Python builtin modules
======================

* multiprocessing: Python 2.6
* concurrent.futures: Python 3.2 (Pool of threads/processes)


Concurrency
===========

* `Unyielding
  <https://glyph.twistedmatrix.com/2014/02/unyielding.html>`_
  by Glyph, a Twisted developer, February 2014
* `The Secret to 10 Million Concurrent Connections -The Kernel is the Problem,
  Not the Solution
  <http://highscalability.com/blog/2013/5/13/the-secret-to-10-million-concurrent-connections-the-kernel-i.html>`_


Issues with eventlet
====================

* `SQLAchemy: MySQLdb + eventlet = sad
  <https://wiki.openstack.org/wiki/Openstack_and_SQLAlchemy#MySQLdb_.2B_eventlet_.3D_sad>`_
* OpenStack reaction `when adding sleep(0) fixes an eventlet test
  <http://openstackreactions.enovance.com/2013/12/when-adding-sleep0-fixes-an-eventlet-test/>`_
* Read "What’s wrong with eventlet?" section of `Use the new asyncio module and
  Trollius in OpenStack
  <http://techs.enovance.com/6562/asyncio-openstack-python3>`_
