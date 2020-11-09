Documenting code with Sphinx
============================

.. note::
   
   This outline needs fleshing out.

One of the most valuable contributions that non-core developers make is
helping keep a project's documentation up-to-date and useful.

Each Zope packages should have its own documentation, managed within the
project itself.  This documentation is maintained as a set of files in the
``docs`` subdirectory of the project, containing source files in
"restructured text" format (see the `reStructuredText Refererence
<https://docutils.sourceforge.io/rst.html>`_) as well as control files
which convert those source texts into HTML, Latex, PDF, etc., using Sphinx
(see the `Sphinx manual <https://www.sphinx-doc.org/en/master/contents.html>`_).

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
   $ git clone https://github.com/zopefoundation/Zope.git
   $ cd Zope/docs
   $ PATH=/opt/Sphinx/bin:$PATH make html

After running that command, you can view the generated docs in your
browser, just open ``/tmp/Zope/docs/_build/html/index.html``

Re-running the ``make html`` command after making changes to the docs lets you
see the rendered HTML corresponding to your updates.

You can also use the Sphinx ``doctest`` extension to test example code
snippets in the documentation:

.. code-block:: sh

   $ PATH=/opt/Sphinx/bin:$PATH make doctest
