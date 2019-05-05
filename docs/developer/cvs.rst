.. _cvs-read-only-checkout:

How-to:  Get a read-only CVS checkout
=====================================

.. note::

   This document is only of importance if you are interested for checking
   out older Zope 2 versions (before Zope 2.8). The current codebase
   is now maintained in the Subversion repository (see
   :ref:`read-only-subversion-checkout`).
  
Anyone can track Zope changes with a read-only checkout of the sources - here
are instructions for hooking it up.

There are several top-level modules in the archives.  Chief among them is the
source for Zope itself:  we'll use that source for our example.

Read-only access is via CVS ``pserver`` mode.

Before you can check anything out, you must have done a CVS "login" to the CVS
``pserver``. You only need to login once per repository per account. To login:

.. code-block:: sh

   $ cvs -d :pserver:anonymous@cvs.zope.org:/cvs-repository login

You will be prompted for a password - anything will satisfy the prompt,
including an empty line.

- The ``-d`` option identifies the repository, indicating ``pserver`` mode,
  user ``anonymous``, host ``cvs.zope.org``, and repository directory
  ``/cvs-repository``.

You only need to log in one time:  CVS then creates a file in your home
directory named ``.cvspass``, containing the login info. All subsequent access
to that repository will use the stashed info.

Once your login is established, you can do your initial check out:

.. code-block:: sh

   $ cvs -z7 -d :pserver:anonymous@cvs.zope.org:/cvs-repository checkout Zope

- ``-z7`` says to use a substantial level of compression, balancing CPU and
  network bandwidth.
  
.. note::
   The module being checked out is  ``Zope``, no longer ``Zope2``. The
   ``Zope2`` section is not maintained, and will eventually be removed.

This should issue lots of check out messages, creating a directory named
``Zope``, with the entire distribution inside it. The initial checkout creates
a copy of the source files together with some CVS bookkeeping, in directories
all named ``CVS``.

Once you've done these initial steps, you can stay current by cd'ing into any
of the created Zope subdirectories and typing:

.. code-block:: sh

   $ cvs -q up -P -d

- ``-q`` says not to spew about unchanged files.
- ``-P`` says to prune empty (eg, obsolete) directories.
- ``-d`` says to check out newly added directories.

In a pinch, you could just do a ``cvs up``, but: you won't get new
directories, nor will defunct directories be removed, and you'll get lots of
unnecessary messages...)

.. note::

   There is truly no reason to document getting a writable CVS checkout,
   because all active development takes place in the Subversion repository
   (see :ref:`subversion-writable-checkout`).
