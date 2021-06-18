Building binary wheels
======================

Several packages in the Zope Foundation repositories contain C code, which
means they should be packaged and published as binary wheels alongside the
standard egg archive. Building binary wheels has its pitfalls, though. If not
done right they can cause application instability and crashes.


.. warning::
    Publishing binary wheels built in a local build environment is highly
    discouraged! Every build environment is different, binary wheels made for
    publication on PyPI should only be built in standardized and predictable
    environments.

To minimize problems we have automated binary wheel building using CI providers
like Appveyor and GitHub Actions. Wheels are built and uploaded using a special
GitHub account named ``zope.wheelbuilder``. These configurations and the PyPI
account are currently maintained by Marius Gedminas, Michael Howitz and Jens
Vagelpohl. You can contact them by posting your question or bug report in the
`meta repository issue tracker
<https://github.com/zopefoundation/meta/issues>`_. Here is a short description
of the process, please note that some steps can only be performed by the
configuration maintainers:

Prerequisites
-------------
- every project publishing binary wheels must add the PyPI account
  ``zope.wheelbuilder`` to the list of project maintainers on PyPI. 
- log into the ``zope.wheelbuilder`` account and create an API token for the
  project on the `Account settings` page with upload permissions and the
  project name as scope. Copy the token value - this is the only time you can.

Using Appveyor
--------------
- log into Appveyor at ci.appveyor.com, click on `Account` at the top and then
  `Encrypt YAML` on the left-hand menu. Paste the copied token into the input
  field and then copy the encrypted value.
- if the project already uses the `standardized parameterized project
  configuration <https://github.com/zopefoundation/meta/tree/master/config>`_
  add the following to the ``.meta.toml`` file in the ``[appveyor]`` section,
  replacing ``<USER>`` with the Appveyor account used and ``<ENCRYPTED TOKEN>``
  with the encrypted value from the previous step. Then rebuild the
  configuration with ``config-package.py`` so the actual ``appveyor.yml`` file
  is updated:

.. code:: ini

    [appveyor]
    global-env-vars = [
        "# Currently the builds use @<USER>'s Appveyor account.  The PyPI token",
        "# belongs to zope.wheelbuilder, managed by @mgedmin and @dataflake.",
        "",
        "global:",
        "  TWINE_USERNAME: __token__",
        "  TWINE_PASSWORD:",
        "    secure: <ENCRYPTED TOKEN>",
        ]

- if you are not using the standardized project config you can edit
  ``appveyor.yml`` directly:

.. code:: yaml

    environment:

      global:
        # Currently the builds use @<USER>'s Appveyor account.  The PyPI token
        # belongs to zope.wheelbuilder, managed by @mgedmin and @dataflake.

        TWINE_USERNAME: __token__
        TWINE_PASSWORD:
          secure: <ENCRYPTED TOKEN>

    <...>

    deploy_script:
      - ps: if ($env:APPVEYOR_REPO_TAG -eq $TRUE) { pip install twine; twine upload --skip-existing dist\*.whl }
    
    deploy: on


Using GitHub Actions
--------------------
- on your project GitHub page go to `Settings` and then click on `Secrets` on
  the left-hand menu. Create a new repository secret and call it
  ``TWINE_PASSWORD``. Paste the API token value you created for the
  ``zope.wheelbuilder`` PyPI account.
- take a look at a `complete GitHub Actions test and wheel building
  configuration
  <https://github.com/zopefoundation/ExtensionClass/blob/master/.github/workflows/tests.yml>`_
  for inspiration, or if you already use the `standardized parameterized project
  configuration <https://github.com/zopefoundation/meta/tree/master/config>`_
  simply build your configuration from the template named `c-code`.
