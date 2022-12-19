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

Now it the time to drop support for Python 2.7 up to 3.6 as they are all
no longer maintained by the Python community and the maintencance burden
has become too heavy.

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

The following steps are necessary to remove support for Python 2.7 up to 3.6
from a package:

- Update version number to next major version::

    $ bumpversion --breaking
    $ addchangelogentry "Drop support for Python 2.7, 3.5, 3.6."

- Remove Python 2 support from the Trove classifiers in ``setup.py`` and update
  ``python_requires``::

    $ check-python-versions --drop 2.7,3.5,3.6

- ``.meta.toml``

  - Remove Python 2 specific settings

- Run ``meta/config`` to remove Python 2 support from other configuration
  files and create a branch::

    $ bin/python config-package.py <PATH-TO-REPOS> --without-legacy-python --no-commit --branch=py3-only

- ``setup.py``

  - Remove ``six`` from the list of dependencies
  - Remove other things pointing to Python 2 or PyPy2.

- Remove Python 2.7 up to 3.6 support code:

  - Update the code to Python 3 only and update usage of ``six``::

    $ find src -name "*.py" -exec pyupgrade --py3-plus --py37-plus {} \;

  - Replace all remaining ``six`` mentions, find it by running::

    $ grep -rn six src

  - Find any remaining code that may support Python 2::

    $ egrep -rn "2.7|3.5|3.6|sys.version|PY2|PY3|Py2|Py3|Python 2|Python 3|__unicode__|ImportError" src

  - Run the tests with ``tox`` and fix any problems you encounter.

- Commit the changes to the branch.

- Create pull request against ``master`` with your changes.
