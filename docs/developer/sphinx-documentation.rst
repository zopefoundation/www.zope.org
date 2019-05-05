Documenting Zope Packages Using Sphinx
======================================

.. note::
   
   This outline needs fleshing out.

One of the most valuable contributions that non-core developers make is
helping keep a project's documentation up-to-date and useful.

Each Zope packages should have its own documentation, managed within the
checkout of the project (see :doc:`noncommitter-svn` and
:doc:`noncommitter-bzr` for notes on getting checkouts / branches as a 
non-committer).

This documentation is maintained as a set of files in the ``docs``
subdirectory of the project, containing source files in "restructured text"
format (see the `reStructuredText Refererence
<http://docutils.sourceforge.net/rst.html>`_) as well as control files
which convert those source texts into HTML, Latex, PDF, etc., using Sphinx
(see the `Sphinx manual <http://sphinx.pocoo.org/contents.html>`_).

The top-level document is conventionally ``docs/index.rst``.  This document
should explain the purpose of the project, and will often link to other
documents outlining usage, APIs, etc.


.. _building-html-docs-plain:

Building the HTML Documentation
-------------------------------

If you have Sphinx installed somewhere on your system, the ``docs/Makefile``
can be used to build various flavors of documentation.  Assuming that the
Sphinx scripts are installed in ``/opt/Sphinx/bin``:

.. code-block:: sh

   $ cd /tmp
   $ svn co svn://svn.zope.org/repos/main/zope.event/trunk event-trunk
   $ cd event-trunk/docs
   $ PATH=/opt/Sphinx/bin:$PATH make html

After running that command, you can view the generated docs in your
browser:  file:///tmp/event-trunk/docs/.build/html/index.html

Re-running the ``make`` command after making changes to the docs lets you
see the rendered HTML corresponding to your updates.

You can also use the Sphinx ``doctest`` extension to test example code
snippets in the documentation:

.. code-block:: sh

   $ PATH=/opt/Sphinx/bin:$PATH make doctest


.. _building-html-docs-buildout:

Building the HTML Documentation using :mod:`zc.buildout`
--------------------------------------------------------

Most Zope projects have support for building and running their tests using
:mod:`zc.buildout`.  Some of them also support building their docs using
:mod:`zc.buildotu`:

.. code-block:: sh

   $ cd /tmp
   $ svn co svn://svn.zope.org/repos/main/zope.event/trunk event-trunk
   $ cd event-trunk
   $ /opt/Python-2.6.5/bin/python bootstrap.py
   ...
   $ bin/buildout
   ...
   $ bin/make-docs

If the ``make-docs`` script isn't included yet, then adding it would be
a really useful contribution.  Add a section like the following to the
project's ``buildout.cfg``:

.. code-block:: ini

   [sphinx]
   recipe = collective.recipe.sphinxbuilder
   build = ${buildout:directory}/docs/_build
   source = ${buildout:directory}/docs
   outputs = doctest html
   script-name = make-docs
   extra-paths = ${buildout:directory}

If your project keeps its top-level package in the ``src`` subdiretory, the
last line of that section would be:

.. code-block:: ini

   extra-paths = ${buildout:directory}/src
