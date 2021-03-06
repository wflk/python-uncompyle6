|buildstatus|

uncompyle6
==========

A native Python cross-version Decompiler and Fragment Decompiler.
Follows in the tradition of decompyle, uncompyle, and uncompyle2.


Introduction
------------

*uncompyle6* translates Python bytecode back into equivalent Python
source code. It accepts bytecodes from Python version 2.3 to 3.5 or
so. The code requires Python 2.6 or later and has been tested on Python
running versions 2.3-2.7, and 3.2-3.5.

Why this?
---------

There were a number of decompyle, uncompile, uncompyle2, uncompyle3
forks around. All of them come basically from the same code base, and
almost all of them no longer maintained or worked on. Only one handled
Python 3, and even there, only 3.2. This code pulls these together,
handles a wide range of bytecodes and addresses a number of open
issues in previous forks.

What makes this different from other CPython bytecode decompilers?  Its
ability to deparse just fragments and give source-code information
around a given bytecode offset.

I use this to deparse fragments of code inside my trepan_
debuggers_. For that, I need to record text fragments for all
bytecode offsets (of interest). This purpose although largely
compatible with the original intention is yet a little bit different.
See this_ for more information.

The idea of Python fragment deparsing given an instruction offset can
be used in showing stack traces or any program that wants to show a
location in more detail than just a line number.  It can be also used
when source-code information does not exist and there is just bytecode
information.

Installation
------------

This uses setup.py, so it follows the standard Python routine:

::

    pip install -r requirements.txt
    pip install -r requirements-dev.txt
    python setup.py install # may need sudo
    # or if you have pyenv:
    python setup.py develop

A GNU makefile is also provided so :code:`make install` (possibly as root or
sudo) will do the steps above.

Testing
-------

::

   make check

A GNU makefile has been added to smooth over setting running the right
command, and running tests from fastest to slowest.

If you have remake_ installed, you can see the list of all tasks
including tests via :code:`remake --tasks`


Usage
-----

Run

::

$ uncompyle6 *compiled-python-file-pyc-or-pyo*

For usage help:

::

   $ uncompyle6 -h


Known Bugs/Restrictions
-----------------------

Python 2 deparsing decompiles and verifies from Python 2.3.7 to Python
3.4.2 on the standard library packages I have on my system.

(Verification is the process of decompiling bytecode, compiling with a
Python for that byecode version, and then comparing the byetcode
produced by the decompiled/compiled program. Some allowance is made
for inessential differences.)

Later distributions average about 200 files. At this point, 2.7
decompilation is better than uncompyle2. A number of bugs have been
fixed.

Python 3.5 largely works, but still has some bugs in it.
Python 3.6 changes things drastically by using word codes rather than
byte codes, and that needs to be addressed.

There is lots to do, so please dig in and help.

See Also
--------

* https://github.com/zrax/pycdc : supports all versions of Python and is written in C++
* https://code.google.com/archive/p/unpyc3/ : supports Python 3.2 only

The above projects use a different decompiling technique what is used here.

The HISTORY file.

.. |downloads| image:: https://img.shields.io/pypi/dd/uncompyle6.svg
.. _trepan: https://pypi.python.org/pypi/trepan
.. _debuggers: https://pypi.python.org/pypi/trepan3k
.. _remake: https://bashdb.sf.net/remake
.. _pycdc: https://github.com/zrax/pycdc
.. _this: https://github.com/rocky/python-uncompyle6/wiki/Deparsing-technology-and-its-use-in-exact-location-reporting
.. |buildstatus| image:: https://travis-ci.org/rocky/python-uncompyle6.svg
		 :target: https://travis-ci.org/rocky/python-uncompyle6
