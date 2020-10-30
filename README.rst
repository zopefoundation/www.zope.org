www.zope.org
============

This repository contains the Sphinx sources for www.zope.org.


Sandbox setup instructions
--------------------------

Create a virtual environment, install ``zc.buildout`` and run the buildout::

  $ python3 -m venv .
  $ bin/pip install -U pip wheel
  $ bin/pip install zc.buildout
  $ bin/buildout


Building the site
-----------------

After the sandbox is set up once (see above), use the following steps to build
the HTML output::

  $ cd docs/
  $ make html

The output will be at ``docs/_build/html``
