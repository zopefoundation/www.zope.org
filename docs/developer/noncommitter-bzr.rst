Contributing as a Non-Committer using Bazaar
============================================

`bzr <http://bazaar-vcs.org/>`_ is one of the current generation of
distributed version control systems (DVCS).

- a `five minute overview
  <http://doc.bazaar.canonical.com/latest/en/mini-tutorial/>`_ of using 
  Bazaar.

- the `Bazaar User Guide
  <http://doc.bazaar.canonical.com/latest/en/user-guide/index.html>`_

.. _branching-bzr:

How-to: Branch using the Bazaar mirror
--------------------------------------

Many Zope projects have a "mirror" of the trunk of their Subversion repository
as a Bazaar branch on Launchpad:

  https://code.launchpad.net/zopetoolkit

  https://code.launchpad.net/zope

The mirror is updated periodically as commits are made to the SVN repository.
You can create a branch from the URLs there as with any other web-hosted
Bazaar branch:

.. code-block:: sh

   $ bzr branch https://code.launchpad.net/zope.event event-trunk

In many cases, this can be shortened to:

.. code-block:: sh

   $ bzr branch lp:zope.event


.. _branching-bzr-svn:

How-to:  Branch with Bazaar directly from Subversion
----------------------------------------------------

Recent versions of bzr and the `bzr-svn plugin
<http://doc.bazaar.canonical.com/plugins/en/svn-plugin.html>`_ allow the
developer to interoperate with a project whose main repository is in
Subversion.  Using this plugin, you can check out the branch from its
native HTTP URL:

.. code-block:: sh

   $ cd ~/zope
   $ bzr branch svn://svn.zope.org/repos/main/zope.event/trunk event-trunk

Inside that branch, you can commit as usual using ``bzr``, but you
won't be able to ``bzr push`` the code back to Subversion unless you
use an ``svn+ssh`` checkout URL, which requires obtaining commit access
to the repository (see :ref:`becoming-a-committer`).

Because all Zope projects are hosted in a centralized repository,
the DVCS needs to pull down lots of information about revisions which aren't
directly related to the branch you want to work on.  In order to keep this
overhead down, especially if you plan to work on multiple Zope projects,
you can create a "shared repository" for your branches before checking
any of them out:

.. code-block:: sh

   $ mkdir ~/zope
   $ cd ~/zope
   $ bzr init-repo
   $ bzr branch lp:zope.event


.. _submitting-patches-bzr:

How-to: Submit a patch from your Bazaar branch
----------------------------------------------

From your Bazaar branch, you can use ``bzr diff`` to create a patch file,
and then submit it just as in :ref:`submitting-patches-svn`.

Bazaar has another feature, ``bzr send``, which you can use to automate
submitting the patch, either via e-mail:

.. code-block:: sh

   $ bzr send --message="Cool feature" --mail-to=maintainer@example.com

or as a file to be uploaded to the bug tracker:

.. code-block:: sh

   $ bzr send --message="Cool feature" -o /tmp/zope.event-my_cool_feature.bzr

In either case, bzr creates a "Bazaar bundle", including both the patch and
extra revision metadata to ease merging your changes using bzr.


.. _pushing-branches-bzr:

How-to:  Push your Bazaar branch to Launchpad
---------------------------------------------

As an alternative to uploading a patch from your Bazaar branch (or
e-mailing it), you can also publish your branch to a server where it
can be cloned over HTTP for others to use, as well as for review and
merging by the package maintainer.

Let's assume that you have been hacking on :mod:`zope.event`, and want to
publish your 'dictchannel' feature branch in hopes of landing it in the next
release.  Let's also assume that you have an account on
`Launchpad <http://launchpad.net/>`_, and want to publish your branch there.

.. code-block:: sh

   $ bzr launchpad-login <userid>
   $ bzr push lp:~<userid>/zope.event/dictchannel

Replace ``<userid>`` with your Launchpad account ID.


.. _requestng-merges:

How-to: Request a merge
-----------------------

After pushing your branch, you can include its URL in an e-mail you send
to the maintainer, requesting a merge of your branch.  You can also link
your branch to a Launchpad issue, as well as using Launchpad's "merge request"
feature to alert the maintainer(s) that your branch is ready to merge.
