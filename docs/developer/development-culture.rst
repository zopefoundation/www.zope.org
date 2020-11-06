Developer guidelines
====================

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

Layout and Conventions
----------------------

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


Python 2 support policy
-----------------------

.. note::
    This policy applies to packages that are direct dependencies of Zope 4

Zope 4 will retain full Python 2 (and Python 3.5) compatibility throughout its
lifetime. That means all its `direct dependencies
<https://zopefoundation.github.io/Zope/releases/4.x/versions-prod.cfg>`_
and (ideally) many popular add-on packages should also continue supporting
Python 2 until Zope 4 reaches end-of-life status.

We encourage all package maintainers to provide Python 2 support on the current
``master`` release branch instead of a separate maintenance branch because a
separate maintenance branch leads to a lot of extra work:

- fixes must be ported between branches

- a contributor may not even be aware of a separate maintenance branch

- at package release time releases need to be cut from both the ``master`` and
  maintenance branches

With that in mind, dropping Python 2 (or Python 3.5) support for a Zope 4
dependency is allowable under the following circumstances:

- there are compelling technical reasons - or -

- the developer who implements the Python 2/Python 3.5 support drop assumes all
  responsibility for creating a suitable maintenance branch, porting fixes to
  it, and making releases from the maintenance branch until Zope 4 support
  ends.
