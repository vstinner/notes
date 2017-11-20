+++++++++
OpenStack
+++++++++

.. image:: openstack.png
   :alt: OpenStack logo
   :align: right
   :target: http://www.openstack.org/

OpenStack
=========

* `OpenStack Releases <http://docs.openstack.org/releases/>`_
* `OpenStack Project Teams
  <https://governance.openstack.org/reference/projects/>`_
* `Code search <http://codesearch.openstack.org/>`_


Oslo Reviews
============

Link to open reviews for Oslo projects, for all branches:

* `oslo-specs
  <https://review.openstack.org/#/q/status:open+project:openstack/oslo-specs,n,z>`_
* `cliff
  <https://review.openstack.org/#/q/status:open+project:openstack/cliff,n,z>`_
* `oslo-incubator
  <https://review.openstack.org/#/q/status:open+project:openstack/oslo-incubator,n,z>`_
* `oslo.concurrency
  <https://review.openstack.org/#/q/status:open+project:openstack/oslo.concurrency,n,z>`_
* `oslo.config
  <https://review.openstack.org/#/q/status:open+project:openstack/oslo.config,n,z>`_
* `oslo.db
  <https://review.openstack.org/#/q/status:open+project:openstack/oslo.db,n,z>`_
* `oslo.i18n
  <https://review.openstack.org/#/q/status:open+project:openstack/oslo.i18n,n,z>`_
* `oslo.log
  <https://review.openstack.org/#/q/status:open+project:openstack/oslo.log,n,z>`_
* `oslo.messaging
  <https://review.openstack.org/#/q/status:open+project:openstack/oslo.messaging,n,z>`_
* `oslo.middleware
  <https://review.openstack.org/#/q/status:open+project:openstack/oslo.middleware,n,z>`_
* `oslo.rootwrap
  <https://review.openstack.org/#/q/status:open+project:openstack/oslo.rootwrap,n,z>`_
* `oslo.serialization
  <https://review.openstack.org/#/q/status:open+project:openstack/oslo.serialization,n,z>`_
* `oslosphinx
  <https://review.openstack.org/#/q/status:open+project:openstack/oslosphinx,n,z>`_
* `oslotest
  <https://review.openstack.org/#/q/status:open+project:openstack/oslotest,n,z>`_
* `oslo.utils
  <https://review.openstack.org/#/q/status:open+project:openstack/oslo.utils,n,z>`_
* `oslo.versionedobjects
  <https://review.openstack.org/#/q/status:open+project:openstack/oslo.versionedobjects,n,z>`_
* `oslo.vmware
  <https://review.openstack.org/#/q/status:open+project:openstack/oslo.vmware,n,z>`_
* `pylockfile
  <https://review.openstack.org/#/q/status:open+project:openstack/pylockfile,n,z>`_
* `stevedore
  <https://review.openstack.org/#/q/status:open+project:openstack/stevedore,n,z>`_
* `taskflow
  <https://review.openstack.org/#/q/status:open+project:openstack/taskflow,n,z>`_

Development tools:

* `hacking
  <https://review.openstack.org/#/q/status:open+project:openstack-dev/hacking,n,z>`_
* `pbr
  <https://review.openstack.org/#/q/status:open+project:openstack-dev/pbr,n,z>`__

Gerrit
======

* Find my own draft comments:
  `Search for 'has:draft reviewer:self'
  <https://review.openstack.org/#/q/has:draft+reviewer:self,n,z>`_
* `Gerrit Workflow <https://wiki.openstack.org/wiki/Gerrit_Workflow>`_
* To run again a failing test on Gerrit, add the following comment:

  - ``recheck`` (or ``recheck no bug``)
  - ``recheck bug <number>`` if you know the bug number
  - note: ``reverify`` is outdated
  - ``check hyper-v``: `Microsoft Hyper-V CI
    <https://wiki.openstack.org/wiki/ThirdPartySystems/Hyper-V_CI>`_:
  - ?: `Intel PCI CI
    <https://wiki.openstack.org/wiki/ThirdPartySystems/Intel-PCI-CI>`_
  - ``recheck-pkvm``: `IBM PowerKVM CI
    <https://wiki.openstack.org/wiki/ThirdPartySystems/IBMPowerKVMCI>`_:
  - ``vmware-recheck-patch``: `VMware NSX CI
    <https://wiki.openstack.org/wiki/NovaVMware/Minesweeper#What_to_do_when_a_build_fails>`_:
  - ``xen: recheck``: `XenProject CI
    <https://wiki.openstack.org/wiki/ThirdPartySystems/XenProject_CI>`_

* `Gerrit: user search documentation
  <https://gerrit.googlesource.com/gerrit/+/master/Documentation/user-search.txt>`_

  * ``project:openstack-infra/project-config message:heat status:open``: open
    patches for the project-config project which contains the word "heat"
    (match the commit message).


Hack OpenStack
==============

* `Gmane: openstack-devel mailing list
  <http://dir.gmane.org/gmane.comp.cloud.openstack.devel>`_
* `Zuul Status <http://status.openstack.org/zuul/>`__
  (other link: `Zuul Status <http://zuul.openstack.org/>`__, raw output?)
* `Hacking Guide <http://docs.openstack.org/developer/hacking/>`_
* `Code Review <https://review.openstack.org/>`_
* `GIT Commit Good Practice
  <https://wiki.openstack.org/wiki/GitCommitMessages>`_:

  - ``Blueprint <name>`` (or ``Implements: blueprint <name>``?),
    ``Partially implements: blueprint <name>``
  - ``Depends-On: Ixxx``
  - ``Closes-Bug: #<bug ID>``, ``Partial-Bug: #<bug ID>``,
    ``Related-Bug: <bug ID>``
  - ``Co-Authored-By: full name <name@example.com>``

* `Developer’s Guide
  <http://docs.openstack.org/infra/manual/developers.html>`_
* `Test Repository <http://testrepository.readthedocs.org/>`_
* `elastic recheck <http://status.openstack.org/elastic-recheck/>`_


Tests
=====

Tools
-----

* `testtools <https://testtools.readthedocs.org/>`_
  (`NEWS <https://github.com/testing-cabal/testtools/blob/master/NEWS>`_):
  extensions to the Python standard library unit testing framework
  (ex: ``testtools.matchers``)
* `testscenarios <https://pypi.python.org/pypi/testscenarios/>`_:
  pyunit extension for dependency injection
* `subunit <https://pypi.python.org/pypi/python-subunit/>`_:
  subunit test (binary) streaming protocol
* `testrepository <https://pypi.python.org/pypi/testrepository>`_:
  test runner to run tests in parallel, ``testr`` is the CLI
  (`testr wiki, not really helpful <https://wiki.openstack.org/wiki/Testr>`_)
* `tox <http://testrun.org/tox/latest/>`_
  (`changelog <https://testrun.org/tox/latest/changelog.html>`_):
  create a environment and run tests

.. seealso::

   `nose usage <https://nose.readthedocs.org/en/latest/usage.html>`_
   and `pbr <http://docs.openstack.org/developer/pbr/>`__ (`github
   <https://github.com/openstack-dev/pbr>`_).

testr: isolate bug
------------------

https://rbtcollins.wordpress.com/2015/12/02/diagnosing-flaky-tests/

Load a subunit file downloaded from OpenStack gates::

    (py27) $ wget http://logs.openstack.org/45/275645/1/check/gate-glance-python27/e3fffca/testrepository.subunit.gz
    (py27) $ gunzip testrepository.subunit.gz
    (py27) $ testr load testrepository.subunit


testr
-----

Run tests:

* run --no-parallel: run all tests in a single process
* testr run --until-failure: run forever, until a test fails

Analyze latest run:

* testr last --subunit|subunit2ls: list tests of the previous run
* testr run --analyze-isolation: try to isolate the failing test, find the
  minimum tests to reproduce the fail

subunit tools:

* subunit-filter
* subunit-ls

Bisection: `diagnosing flaky tests
<https://rbtcollins.wordpress.com/2015/12/02/diagnosing-flaky-tests/>`_.


notes
-----

Run unit tests::

    . .tox/py27/bin/activate
    testr run

Shell commands to run unit tests::

        set -e && \
                TEMP_REZ=`mktemp -t` && \
                python setup.py testr --slowest --testr-args='--subunit  ' \
                        | tee $$TEMP_REZ | subunit2pyunit || true ; \
                cat $$TEMP_REZ | subunit-filter -s --no-passthrough | subunit-stats ; \
                rm -f $$TEMP_REZ ;

* ``--slowest`` shows the statistics at the end of the test run. Nothing fancy.
* ``--testr-args='--subunit`` tells testr to output a subunit2 format for its
  unit tests. subunit2 format is a BINARY format, which you shouldn't output to
  the screen.
* subunit2pyunit will convert that to a nicer output
* ``tee $$TEMP_REZ`` .. ``cat $$TEMP_REZ | subunit-filter -s --no-passthrough | subunit-stats``
  shows the nice statistics about the test run (eg: how many tests in total,
  how many skips, how many failed, how many success)


testr: list skipped tests
=========================

::

    testr last --subunit|subunit-filter -s|subunit-ls >A
    testr last --subunit|subunit-filter -s --no-skip|subunit-ls >B
    diff -u A B


tox/testr: "db type could not be determined" error
==================================================


testr uses a database to store test results. If the database is created by
Python 2, Python 3 cannot read it and then you get the error "db type could not
be determined".

Workaround: remove ``.testrepository`` directory and rerun tox again.


tox/testr: "gdbm is missing"
============================

If you run ``tox -e py34`` and then ``tox -e py27``, the second commands may
fail because Python 2.7 does not have the gdbm module.

On Ubuntu, type::

    sudo apt-get install -y python-gdbm


testr: "local variable 'run_subunit_content' referenced before assignment" error
================================================================================

See `Error message opaque when .testrepository files are unreadable
<https://bugs.launchpad.net/testrepository/+bug/1348970>`_.


Re-run a single failing test
============================

testtools
---------

Re-run a single test with testtools::

   $ tox -e py33
   ...
   FAIL: tests.test_swiftclient.TestPutObject.test_unicode_ok
   ...
   $ . .tox/py33/bin/activate
   $ python -m testtools.run tests.test_swiftclient.TestPutObject.test_unicode_ok
    Tests running...
    ======================================================================
    FAIL: tests.test_swiftclient.TestPutObject.test_unicode_ok
    ----------------------------------------------------------------------
    ...
    Ran 1 test in 0.002s


tox
---

Re-run a single test with tox+testr::

   $ tox -e py33
   ...
   FAIL: tests.test_swiftclient.TestPutObject.test_unicode_ok
   ...
   $ tox -e py33 -- --isolated tests.test_swiftclient.TestPutObject.test_unicode_ok
   ...
   FAIL: tests.test_swiftclient.TestPutObject.test_unicode_ok
   ...

.. note::

   Enter the virtualenv and type ``testr run
   tests.test_swiftclient.TestPutObject.test_unicode_ok`` should work, but it
   doesn't in the Python 3.3 virtual environment of python-sphinxclient?!


nose
----

Re-run a single test with nose::

   $ nosetests
   ...
   ======================================================================
   FAIL: tests.test_command_helpers.TestStatHelpers.test_stat_account_human
   ----------------------------------------------------------------------
   ...

   $ nosetests tests.test_command_helpers:TestStatHelpers.test_stat_account_human


Test issues
===========

* `Cryptic error from subunit when an import fails
  <https://bugs.launchpad.net/testrepository/+bug/1271133>`_

  - subunit: https://code.launchpad.net/~alexei-kornienko/subunit/bug-1271133
  - testrepository: https://code.launchpad.net/~alexei-kornienko/testrepository/bug-1271133
  - testtools: `Added verbose error information <https://github.com/testing-cabal/testtools/pull/77>`_

    * Python: `No introspective way to detect ModuleImportFailure in unittest <http://bugs.python.org/issue19746>`_

* https://code.launchpad.net/~sileht/testscenarios/testscenarios/+merge/211038


RabbitMQ
========

Type::

    dnf install -y rabbitmq-server
    vim /etc/rabbitmq/rabbitmq.config
    # in "{rabbit," uncomment:
    #    {loopback_users, []}
    # (no trailing comma ",")
    sudo systemctl restart rabbitmq-server
    sudo systemctl status rabbitmq-server
    sudo rabbitmqctl change_password guest password


DevStack
========

To install Fedora:

* Download boot ISO at https://boot.fedoraproject.org/
* Select Install Supported Fedora
* In the installer GUI, select packages: (o) Minimal Install
* Create user haypo
* Reboot
* Log as root
* vi /etc/group: add haypo to wheel: line
* Log as haypo
* sudo dnf install -y git tmux
* git clone https://git.openstack.org/openstack-dev/devstack


OpenStack openstack_citest
==========================

For MySQL you can use the following commands::

    mysql -u root
    mysql> CREATE USER 'openstack_citest'@'localhost' IDENTIFIED BY
           'openstack_citest';
    mysql> GRANT ALL PRIVILEGES ON * . * TO 'openstack_citest'@'localhost';
    mysql> FLUSH PRIVILEGES;

http://docs.openstack.org/developer/oslo.db/contributing.html#how-to-run-unit-tests


Ceilometer
==========

Install dependencies::

    sudo yum install mariadb-devel mongodb-server rabbitmq-server

Start MongoDB server::

    sudo systemctl start mongod
    sudo systemctl start rabbitmq-server

Copy Ceilometer config::

    tox -e genconfig
    sudo mkdir /etc/ceilometer
    sudo cp -R etc/ceilometer/ /etc/ceilometer/

Configure Ceilometer database::

    [database]
    connection = mongodb://127.0.0.1:27017/ceilometer

Create the DB::

    ceilometer-dbsync

Run collector in debug::

    ceilometer-collector -d

Send a sample::

    ceilometer-send-sample --sample-name name --sample-resource resource

Show meters in MongoDB::

    $ mongo
    > use ceilometer
    > db.meter.find()
    (...)
    ^D

Note: If you get the error "mongo: symbol lookup error: mongo: undefined
symbol: _ZN2v86LockerC1EPNS_7IsolateE" when running the "mongo" command, see
the bug `mongo client lookup error
<https://bugzilla.redhat.com/show_bug.cgi?id=973843>`_. The bug occurs if you
installed the package "v8" from the Chromium repository.
