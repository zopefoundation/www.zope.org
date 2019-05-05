Zope Development Culture
========================

.. _coding-standards:

Coding Standards
----------------

As a general rule, projects in the ``Zope`` repository abide by the
following standards:

- Code in Zope-related projects should generally conform to `PEP 8 coding
  style <http://www.python.org/dev/peps/pep-0008/>`_. In
  particular, *Python code should never exceed 80 columns*.  Existing
  code should be updated to this standard only conservatively, to ease
  integration of patches made against older releases.

- Project trunks should be kept in "ready-to-release" state:  all unit
  tests pass, changelogs are kept updated, etc.

- We prefer that each project's unit tests be runnable using the default
  :mod:`setuptools` testrunner:

  .. code-block: sh

     $ /path/to/python setup.py test

- Integation or functional tests may require a more elaborate test runner,
  such as the one provided by :mod:`zope.testrunner`.  Most projects have
  built-in support for setting up this testrunner using :mod:`zc.buildout`.
  (see :ref:`using-buildout`).

- All features and APIs should be fully documented using Sphinx.

- Solid release management, including releases to PyPI corresponding to
  "pristine" tags, detailed change logs, etc.

While some older projects may not be completely in line with this
culture, we are committed to moving them all closer with any change.
As a corollary:  if you are submitting a patch to a project in this
repository, and you want to expedite its acceptance, ensure that your patch
maintains or improves the target project's conformance to these goals.

See these other resources on coding style in Zope projects:

- `Zope3 Coding Standards <http://wiki.zope.org/zope3/CodingStyle>`_

- `Zope Toolkit Coding Style <http://docs.zope.org/zopetoolkit/codingstyle/index.html>`_


.. _layout-conventions:

Layout and Conventions
----------------------

Each project should consist of a single, top-level project folder in
Subversion, containing three conventional folders:  ``trunk``, where the
majority of development work occurs, ``tags``, containing the "pristine"
tags made when releasing the project, and ``branches``, containing both
"maintenance" branches where bug fixes to a released version might be
made, and "development" branches, for work which would otherwise de-
stabilize the trunk.

Because we are mostly working on Python code here, the trunk and folders
under the ``tags`` or ``branches`` folders are normally arranged as a
:mod:`distutils` project, e.g.::

  <directory>
  - setup.py
  - README.txt
  - CHANGES.txt
  + docs/
    - Makefile
    - conf.py
    - index.rst
    - api.rst
    + .static/
    + .build/
    + .templates/
  + package/
    - __init__.py
    + subpacakge/
      - __init__.py
      - module.py
      + tests/
        - __init__.py
        - test_module.py
      + templates/
        - template.pt

Many packages place the first-level ``package`` directory in a ``src``
subdirectory inside the checkout.


.. _using-buildout:

Running Tests using :mod:`zc.buildout`
--------------------------------------

Most projects in the Zope repository are already configured to support
building in-place and running tests using :mod:`zc.buildout`.

.. code-block:: sh

   $ svn co svn://svn.zope.org/repos/main/zope.event/trunk event-trunk
   $ cd event-trunk
   $ /opt/Python-2.6.5/bin/python bootstrap.py
   ...
   Generated script '/tmp/event-trunk/bin/buildout'.
   $ bin/buidout
   Develop: '/tmp/event-trunk/.'
   ...
   Generated script '/tmp/event-trunk/bin/test'.
   $ bin/test --all
   Running zope.testing.testrunner.layer.UnitTests tests:
     Set up zope.testing.testrunner.layer.UnitTests in 0.000 seconds.
     Ran 3 tests with 0 failures and 0 errors in 0.006 seconds.
   Tearing down left over layers:
     Tear down zope.testing.testrunner.layer.UnitTests in 0.000 seconds.


