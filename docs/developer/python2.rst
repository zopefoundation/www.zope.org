Python 2 support
================

.. note::
    This document is relevant for packages that are either direct dependencies
    of Zope version 4 or popular add-ons for Zope version 4 and their
    dependencies.

Zope 4 will retain full Python 2 (and Python 3.5) compatibility throughout its
lifetime. That means all its `direct dependencies
<https://zopefoundation.github.io/Zope/releases/4.x/versions-prod.cfg>`_
and (ideally) many popular add-on packages should also continue supporting
Python 2 and Python 3.5 until Zope 4 reaches end-of-life status.


When to drop support
--------------------

We encourage all package maintainers to provide Python 2 support on the
``master`` release branch instead of a separate maintenance branch because a
separate maintenance branch leads to a lot of extra work:

- fixes must be ported between branches

- a contributor may not even be aware of a separate maintenance branch

- at package release time releases need to be cut from both the ``master`` and
  maintenance branches

- since existing tools for finding updated dependencies for Zope 4 only detect
  the very latest releases, which may no longer support Python 2, every single
  dependency that is pinned to an earlier version must be manually checked to
  see if there are updates.

With that in mind, dropping Python 2 (or Python 3.5) support for a Zope 4
dependency is allowable under the following circumstances:

- there are compelling technical reasons - or -

- the developer who implements the Python 2/Python 3.5 support drop assumes all
  responsibility for creating a suitable maintenance branch, porting fixes to
  it, and making releases from the maintenance branch until Zope 4 support
  ends.


How to drop support
-------------------

When dropping Python 2 support you should also "upgrade" the code to support
more modern practices, like using `f-strings
<https://www.python.org/dev/peps/pep-0498/>`_.

Prerequisites
~~~~~~~~~~~~~

- ``pyupgrade`` installed (the code examples below expect it to be on the
  search PATH.)


Typical steps
~~~~~~~~~~~~~

The following steps are necessary to remove Python 2 support from a package:

- Create a new branch from ``master`` first that can be used as maintenance
  branch with Python 2 support for backporting important fixes if needed.

- Create a new branch from ``master`` to hold your code changes and switch to
  that branch for the next steps.

- ``setup.py``

  - Update version number to next major version.
  - Remove Python 2 from the list of classifiers.
  - Remove ``six`` from the list of dependencies
  - Update ``python_requires`` to ``python_requires='>=3.6, <4'``
  - Remove other things pointing to Python 2 or PyPy/PyPy2.

- ``setup.cfg``

  - set ``universal = 0`` in section ``[bdist_wheel]``

- ``tox.ini``

  - Remove ``py27``, ``pypy`` or ``pypy2`` from ``envlist``
  - Remove Python 2 specific environments

- ``.travis.yml``

  - Remove Python 2.7 and PyPy/PyPy2 jobs.

- ``appveyor.yml``

  - Remove Python 2 job(s) if existing.

- ``CHANGES.rst``

  - Update the version number of the unreleased version
  - Add an entry: ``Drop support for Python 2.``

- Remove Python 2 support code

  - Replace all code that uses ``six`` with its Python 3 equivalent,
    find it by running ``grep -rn six src``
  - Run the tests with ``tox`` and fix any problems you encounter
  - Run ``egrep -rn "2.7|sys.version|PY2|PY3|Py2|Py3|Python 2|Python 3|__unicode__|ImportError" src`` to find any remaining code that may support Python 2
  - Run ``find src -name "*.py" -exec pyupgrade --py36-plus {} \;``
    to update the code to Python 3 only coding standards.

- Create pull request against ``master`` from your code change branch.
