Zope release schedule
=====================

The Zope development and support roadmap. **Last updated: March 2025**

If you use Plone, please visit the `Plone release schedule
<https://plone.org/download/release-schedule>`_ for all Plone-specific details.
Support for Zope releases aims to track support for the respective Plone
version(s) built on top of them.

Zope currently has two release managers, Michael Howitz and Jens Vagelpohl.

.. contents:: Table of contents:
   :local:
   :depth: 1


Support schedule
----------------

.. note::

    The end dates for Zope 5 maintenance and security support represent the
    **earliest dates** for ending support **after Zope 6 is released**. There
    are no firm plans for a Zope 6 release at this time, which means Zope 5
    will be supported longer than stated here.


.. image:: /_static/releases.png

+------+-------+-------------+-----------+----------+------------+------------+
|Series|Latest |Python       |Status     |First     |End support:|End support:|
+------+-------+-------------+-----------+----------+------------+------------+
|      |release|versions     |           |release   |maintenance |security    |
+======+=======+=============+===========+==========+============+============+
|2.13  |2.13.30|2.7          |end of life|2010-11-05|2019-02-09  |2020-12-31  |
+------+-------+-------------+-----------+----------+------------+------------+
|4.0   |4.8.11 |2.7, 3.5-3.8 |end of life|2019-05-10|2021-09-30  |2022-12-31  |
+------+-------+-------------+-----------+----------+------------+------------+
|5.0   |5.13   |3.9-3.13     |maintenance|2020-10-08|2025-12-31  |2026-12-31  |
|      |       |[1]_ [2]_    |           |          |[3]_        |[3]_        |
+------+-------+-------------+-----------+----------+------------+------------+
|6.0   |\-     |TBD          |unreleased |TBD [4]_  |TBD [4]_    | TBD [4]_   |
+------+-------+-------------+-----------+----------+------------+------------+

.. [1] Python 3.10 support added with release 5.4.
       Python 3.11 support added with release 5.7.
       Python 3.12 support added with release 5.9.
       Python 3.13 support added with release 5.11.

.. [2] Python 3.6 support removed with release 5.8.
       Python 3.7 support removed with release 5.11.
       Python 3.8 support removed with release 5.13.

.. [3] Tentative **minimum** support duration and subject to change/extension:
       Final support deadlines for the Zope 5 series will be set when Zope 6 is
       released. Zope 5 will enjoy full maintenance support at least until
       Zope 6 is released and Security support for at least one year after
       that.

.. [4] There are no set plans for a Zope 6 release yet. Final support periods
       for both Zope 5 and Zope 6 will be set once Zope 6 is released and
       follow the `Maintenance policy` guidelines shown below.


Definitions
-----------
On this page, we use these terms:

- *End of Life*: No further development is done and no releases are published.
- *Maintenance support*: security and other bug fixes and small new features
  are added. Around the end of maintenance support, a last release will be done.
- *Security support*: security fixes will be made available for this series.
- *Major* version: 4.0, 5.0
- *Minor* version: 4.5, 5.7
- *Bugfix* version: 4.4.1, 5.6.1


Release cadence
---------------
This is the expected release cadence for Zope:

- We aim to release a new minor version roughly every 2-6 months.
- We aim to release a new major version roughly every 2-3 years.
- Planning for a new minor or major version usually starts after a release has
  been done. Currently, there is no clear calendar with expected dates.


Maintenance policy
------------------
These are the general rules for maintenance support for Zope:

- Each major release series gets at least two years of maintenance support,
  most likely more.
- Maintenance support is extended at least until a new major release is
  published.
- If a new major release is published after the two year maintenance support
  window, the previous release series may be downgraded to Security support
  soon thereafter.


Security policy
---------------
These are the general rules for security support for Zope:

- Each major release gets at least three years of security support.
- There is a security support overlap of at least one year between major
  versions. This gives you time to migrate to a new major version.
- You have to be on the last minor release to have the full period of security
  support.
- Each minor release gets at least one year of security support.
- Note that underlying versions of Python and other dependencies may be out of
  security support sooner.

Versioning policy
-----------------
Zope and Zope ecosystem packages follow `semantic versioning
<https://semver.org/>`_: a new feature means a minor release, a breaking change
means a major release for a package.

- 5.0.1 and 5.0.2 are examples of bugfix releases. These contain bug fixes.
  They may contain new code that should not affect stability, for example
  updated dependency versions. Add-ons should not need changes.
- 5.1 and 5.2 are minor releases. These contain larger changes or new
  backwards-compatible features. Occasionally a minor release may drop
  support for a Python version, if this version is no longer supported by the
  Python community. Minor releases may also add support for newer Python
  versions. Both dropped and added Python version support will be clearly
  visible in the support table above. Add-ons may need to be changed to use the
  new features or Python version. It should be easy to make the same version of
  an add-on work in all minor releases.
- 4 and 5 are major releases. These contain breaking changes. Add-ons are
  likely to need changes. It may be hard to have one version of an add-on work
  across two major versions.

Note that Zope is both a framework and a product, and you can use a lot of
community add-ons and own code on top of it. This means that even a seemingly
innocent fix like adding a class in HTML could break something for someone.
We cannot foresee everything. Please be a bit forgiving.

General advice for all Zope versions
------------------------------------
- Zope 4 has reached end-of-life status. Migrate to Zope 5 as soon as you can.
- Use the **highest Python version** that is supported by your Zope version.
  For release schedules of core Python, see https://www.python.org/downloads/
- Zope 4 and Zope 5 users should upgrade to at least Python 3.7 **as soon as
  possible** to mitigate an `unfixed security issue in the waitress WSGI server
  <https://github.com/Pylons/waitress/security/advisories/GHSA-4f7p-27jc-3c36>`_.
- Regularly check the Zope release page at https://pypi.org/project/Zope/ to
  see if any security fixes are available for your Zope version.


Supported Zope versions
-----------------------

Zope 5
~~~~~~
- First official release: 5.0, October 2020
- Current release: 5.13, March 2025
- Next release expected: Late spring 2025, roughly every 2-6 months.
- Supports Python 3.9, 3.10, 3.11, 3.12 and 3.13.

  - Python 3.6 support was removed in release 5.8.
  - Python 3.7 support was removed in release 5.11.
  - Python 3.8 support was removed in release 5.13.
  - Python 3.10 support was added in release 5.4.
  - Python 3.11 support was added in release 5.7.
  - Python 3.12 support was added in release 5.9.
  - Python 3.13 support was added in release 5.11.

- Used by Plone 6
- Maintenance support until at least December 31, 2025.
- Security support until at least December 31, 2026.



No longer supported Zope versions
---------------------------------

Zope 4
~~~~~~
Zope 4 supports Python 2 and Python 3. It is meant to act as a bridge for those
upgrading applications from Zope 2. Once you are on Zope 4 and Python 3 the
next step to Zope 5 is painless and you should migrate **immediately**.

- First official release: 4.0, May 2019
- Current release: 4.8.11, October 2023
- Next release expected: Zope 4 has reached end-of-life. There **may** be
  sporadic releases to fix urgent issues. Please move to Zope 5.
- Supports Python 2.7, 3.5, 3.6, 3.7 and 3.8.

  - Please note that Python 2.7, 3.5, 3.6 and 3.7 have reached end of life, you
    should use Python 3.8.

- Used by Plone 5.2
- Maintenance support has ended September 30, 2021
- Security support has ended on December 31, 2022.


Zope 2.13
~~~~~~~~~
- First official release: 2.13.0, November 2010
- Last release: 2.13.30, February 2020
- Supports Python 2.7
- Used by Plone 4.3, 5.0 and 5.1
- Maintenance support has ended on February 9, 2019
- Security support has ended on December 31, 2020
