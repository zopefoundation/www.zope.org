Building binary wheels
======================

Several packages in the Zope Foundation repositories contain C code, which
means they should be packaged and published as binary wheels. Building such
binary wheels has its pitfalls, though. If not done right they can cause
application instability and crashes.


.. warning::
    Publishing binary wheels built in a local build environment is highly
    discouraged! Every build environment is different, binary wheels made for
    publication on PyPI should only be built in standardized and predictable
    environments.

To minimize problems we have automated binary wheel building using GitHub
Actions. Wheels are built and uploaded using a special
PyPI account named ``zope.wheelbuilder``. These configurations and the PyPI
account are currently maintained by Marius Gedminas, Michael Howitz and Jens
Vagelpohl. You can contact them by posting your question or bug report in the
`meta repository issue tracker
<https://github.com/zopefoundation/meta/issues>`_. Here is a short description
of the process, please note that some steps can only be performed by the
configuration maintainers:

Prerequisites
-------------
- Every project publishing binary wheels must add the PyPI account
  ``zope.wheelbuilder`` to the list of project maintainers on PyPI. 
- Log into the ``zope.wheelbuilder`` account and create an API token for the
  project on the "Account settings" page with upload permissions and the
  project name as scope. Copy the token value - this is the only time you can.


Using GitHub Actions
--------------------
- On your project GitHub page go to "Settings" and then click on "Secrets" on
  the left-hand menu. Create a new repository secret and call it
  ``TWINE_PASSWORD``. Paste the API token value you created for the
  ``zope.wheelbuilder`` PyPI account.
- Take a look at a `complete GitHub Actions test and wheel building
  configuration
  <https://github.com/zopefoundation/ExtensionClass/blob/master/.github/workflows/tests.yml>`_
  for inspiration, or if you already use the `standardized parameterized project
  configuration <https://github.com/zopefoundation/meta/tree/master/config>`_
  simply build your configuration from the template named `c-code`.
