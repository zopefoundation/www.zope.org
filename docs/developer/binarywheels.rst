Building binary wheels
======================

Several packages in the Zope Foundation repositories contain C code, which
means they should be packaged and published as binary wheels. Building such
binary wheels has its pitfalls, though. If not done right they can cause
application instability and crashes.


.. warning::

    Do not publish binary wheels created in a local build environment to PyPI!
    Every build environment is different, binary wheels made for publication
    on PyPI should only be built in standardized and predictable environments.

Binary wheel building and publishing for Zope Foundation projects is done as
part of the GitHub Actions tests automation. Publishing is done automatically
whenever a tag is pushed to a repository that uses C code extensions. To
prevent supply chain attacks, this publishing process requires manual approval
by at least one member of the GitHub group ``release-managers`` in the
``zopefoundation`` organization.

Here is a short description of the process for repository and PyPI project
admins:

Prerequisites
-------------
- The project is maintained using `zope.meta
  <https://zopemeta.readthedocs.io/>`_ and uses the ``c-code`` template.

Set up steps on GitHub
----------------------
- Log into GitHub, visit the repository settings page and click on
  `Environments` on the left.
- Create an environment named `pypi` and enable `Required reviewers` in the
  `Deployment protection rules` section. Add at least the group
  ``zopefoundation/release-managers`` and click `Save protection rules`.

Setup steps on PyPI
-------------------
- Log into PyPI, visit the project's page and click on `Manage project`.
- Select `Publishing` and fill in the `Add a new publisher` form:

  - Owner: ``zopefoundation``
  - Repository name: The name of the repository
  - Workflow name: ``tests.yml``
  - Environment name: ``pypi``

  Click `Add` and the project is all set for using the Trusted Publishing
  mechanism.
