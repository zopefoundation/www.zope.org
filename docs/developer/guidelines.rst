Developer guidelines
====================

.. note::
    Any code contributions that are more than trivial typo fixes require
    a signed contributor agreement. Please see :doc:`becoming-a-committer`
    for details.


Pull requests
-------------

Pull requests for bug fixes, features or documentation are always welcome.
Here's how you can make it easy to accept your contribution:

- Please create branches in the package's repository instead of forking the
  package. That way other contributors can help easily.

- Respect the conventions you find in the package you're contributing to. This
  includes code style, tools used to run and configure tests, the package
  structure and its management. Coordinate with other developers for that
  package before changing any of these.

- Keep cosmetic and code changes apart. If necessary, put them in separate pull
  requests.

- If your code is fixing a bug it should have unit tests that exercise the
  bug and pass with your fix.

- Make sure all unit and functional tests pass before creating a pull request.
  Most repositories will have a ``tox.ini`` configuration file and you can run
  all tests at once using ``tox``.

- "vendoring in" of third-party code is not allowed unless all contributors to
  that code have also signed a contributor agreement.

Please wait for approval from at least one other contributor before merging
your code, which you can do yourself.


.. _coding-standards:

Coding Standards
----------------

As a general rule, projects in our repositories abide by the
following standards:

- Code in Zope-related projects should generally conform to `PEP 8 coding
  style <https://www.python.org/dev/peps/pep-0008/>`_. In
  particular, *Python code should never exceed 80 columns*.  Existing
  code should be updated to this standard only conservatively, to ease
  integration of patches made against older releases.

- Project `master` branches and all branches that are officially supported
  should be kept in "ready-to-release" state: all unit tests pass, changelogs
  are kept updated, etc.

- All features and APIs should be fully documented using Sphinx.

- Solid release management, including releases to PyPI corresponding to
  "pristine" tags, detailed change logs, etc.

While some older projects may not be completely in line with this
culture, we are committed to moving them all closer with any change.
As a corollary:  if you are submitting a patch to a project in this
repository, and you want to expedite its acceptance, ensure that your patch
maintains or improves the target project's conformance to these goals.


.. _layout-conventions:

Package layout
--------------

Each project should consist of a single, top-level project folder in
GitHub. Because we are mostly working on Python code here, projects are
normally arranged as a :mod:`distutils` project, e.g.::

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

   $ git clone https://github.com/zopefoundation/Zope.git
   $ cd Zope
   $ python3 -m venv .
   $ bin/pip install -U pip wheel zc.buildout
   $ bin/buildout
   ...
   $ bin/test
   ...
