The World of Zope
=================

.. sidebar:: A Bit of History

   In 1996 Jim Fulton, now Zope Corporation CTO, was drafted to teach a
   class on common gateway interface (CGI) programming, despite not
   knowing very much about the subject. CGI programming is a
   commonly-used web development model that allows developers to
   construct dynamic web sites. Traveling to the class, Jim studied all
   the existing documentation on CGI. On the way back, Jim considered
   what he didn't like about traditional CGI-based programming
   environments. From these initial musings the core of Zope was written
   while flying back from the CGI class.

   Zope Corporation (then known as Digital Creations) went on to release
   three open-source software packages to support web publishing: Bobo,
   Document Template, and BoboPOS. These packages were written in a
   language called Python, and provided a web publishing facility, text
   templating, and an object database, respectively. Digital Creations
   developed a commercial application server based on these components
   and called it Principia. In November of 1998, investor Hadar Pedhazur
   convinced Digital Creations to open source Principia, thereby creating
   the foundation for the Zope application server.

   In 2001, the Zope community began working on a component architecture
   for Zope, but after several years they ended up with something much
   more: Zope 3. While Zope 2 was powerful and popular, Zope 3 was
   designed to bring web application development to the next level.

During more than a decade Zope Corp. and the Zope Community have grown
an outstanding set of products and technologies, influencing the
general development of Python based Web application servers and tools.

Frameworks
----------

ZCA
  The Zope Component Architecture provides facilities for defining,
  registering and looking up components. It's perfect for building
  enterprise applications based on loosely coupled components.

  More information at the `zope.component documentation
  <https://zopecomponent.readthedocs.io>`_ and `zope.interface
  documentation <https://zopeinterface.readthedocs.io>`_.

ZTK
  The Zope Toolkit (ZTK) is a set of libraries intended for reuse by
  projects to develop web applications or web frameworks. The ZCA is
  part of it.

  More information at the `Zopetoolkit documentation
  <https://zopetoolkit.readthedocs.io/en/latest/>`_.

ZPT
  Zope Page Templates is Zope's templating mechanism.

  More information at the
  https://zope.readthedocs.io/en/latest/zopebook/AppendixC.html. An alternative
  implementation is provided by `Chameleon
  <https://chameleon.readthedocs.io/en/latest/>`_.

CMF
  The Content Management Framework (CMF) for Zope provides libraries 
  for building content management applications
  together with the Zope Application Server.

Repoze
  Repoze integrates Zope technologies with WSGI and reusable Python middleware.

  More information at https://repoze.org


Databases
---------

ZODB
  The Z Object Database (ZODB) is a native object database, that
  stores your objects while allowing you to work with any paradigms
  that can be expressed in Python.

  More information at https://zodb.org

Application Servers
-------------------

Zope
  Zope is a Python-based application server for building secure and
  highly scalable web applications.

  More information at https://zope.readthedocs.io

Tools
-----
Buildout
  Buildout is a Python-based build system for creating, assembling and
  deploying applications from multiple parts, some of which may be
  non-Python-based.

  More information at https://buildout.org
