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

- Installed packages the code examples below expect it to be on ``$PATH``.

  - ``pyupgrade``
  - ``check-python-versions``
  - ``zest.releaser``

- Repository is under control of ``meta/config`` thus it has a ``.meta.toml``
  file.


Typical steps
~~~~~~~~~~~~~

The following steps are necessary to remove Python 2 support from a package:

- Update version number to next major version::

    $ bumpversion --breaking

- Remove Python 2 support from the Trove classifiers in ``setup.py`` and update
  ``python_requires``::

    $ check-python-versions --drop 2.7,3.5

- ``.meta.toml``

  - Remove Python 2 specific settings

- Run ``meta/config`` to remove Python 2 support from other configuration
  files and create a branch::

    $ bin/python config-package.py <PATH-TO-REPOS> --without-legacy-python --no-commit --branch=py3-only

- ``setup.py``

  - Remove ``six`` from the list of dependencies
  - Remove other things pointing to Python 2 or PyPy2.

- ``CHANGES.rst``

  - Add an entry: ``Drop support for Python 2 and 3.5.``

- Remove Python 2 support code:

  - Update the code to Python 3 only and update usage of ``six``::

    $ find src -name "*.py" -exec pyupgrade --py3-plus --py36-plus {} \;

  - Replace all remaining ``six`` mentions, find it by running::

    $ grep -rn six src

  - Find any remaining code that may support Python 2::

    $ egrep -rn "2.7|3.5|sys.version|PY2|PY3|Py2|Py3|Python 2|Python 3|__unicode__|ImportError" src

  - Run the tests with ``tox`` and fix any problems you encounter.

- Commit the changes to the branch.

- Create pull request against ``master`` with your changes.
