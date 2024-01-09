www.zope.org/www.zope.dev
=========================

This repository contains the Sphinx sources for www.zope.org/www.zope.dev.


Sandbox setup instructions
--------------------------

Create a virtual environment and install the additional requirements from
``requirements.txt``::

  $ python3 -m venv .
  $ bin/pip install -U pip wheel
  $ bin/pip install -Ur requirements.txt


Building the site
-----------------

After the sandbox is set up once (see above), use the following steps to build
the HTML output::

  $ cd docs/
  $ make html

The output will be at ``docs/_build/html``
