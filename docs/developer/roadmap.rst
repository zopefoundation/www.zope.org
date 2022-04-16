Zope development roadmap
========================

The Zope development and support roadmap. **Last updated: April 2022**

If you use Plone, please visit the `Plone release schedule
<https://plone.org/download/release-schedule>`_ for all Plone-specific details.
Support for Zope releases aims to track support for the respective Plone
version(s) built on top of them.


.. warning::

    Zope used to have a policy whereby a given Zope release series will not
    drop support for any Python version it supported at the start of the
    release series. Such a change would require a new major Zope release.
    However, given how fast Python releases are coming, we cannot follow that
    policy anymore.

    Starting with Zope 5, when a Python version reaches End Of Life status,
    we may remove support for it in a following feature (minor) release. This
    is the planned support drop schedule:

    - Python 3.6 support was deprecated with Zope version 5.5.1 and will
      be dropped by Zope version 5.7.


Zope 6 - future version
-----------------------
At this moment there are no planned or actual changes that introduce backwards
incompatibilities and thus merit a new major version, so there is no planned
release date for Zope 6. All development still happens on Zope 5.


Zope 5 - stable version
-----------------------
Plone 6, which is still under development, will use Zope 5.

* Python support:
    - 3.6 (Deprecated with Zope version 5.5.1, will be dropped in Zope version 5.7)
    - 3.7
    - 3.8
    - 3.9
    - 3.10 (new with Zope version 5.4)

* Support schedule:
    - Full support: ongoing
    - Bug fixes: ongoing
    - Security fixes: ongoing


Zope 4 - previous version
-------------------------
The Plone 5.2 release series, which is the current stable release series for
Plone, uses Zope 4.

* Python support:
    - 2.7
    - 3.5
    - 3.6
    - 3.7
    - 3.8

* Support schedule:
    - Full support: ended on 2020-10-08 (the Zope 5.0 release date)
    - Bug fixes: until 2022-12-31
    - Security fixes: until 2022-12-31


Zope 2.13 - old version
-----------------------
Plone 4.3, 5.0 and 5.1 are running on top of Zope 2.13. Zope 2.13 is no longer
officially supported.

* Python support:
    - 2.7

* Support schedule:
    - Full support: ended
    - Bug fixes: ended
    - Security fixes: ended
