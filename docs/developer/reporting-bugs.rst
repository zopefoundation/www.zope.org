Reporting Bugs against Zope Packages
====================================

.. note::
   
   This outline needs fleshing out.


Identifying the Project which Has the Bug
-----------------------------------------

- Look at tracebacks from "bottom up".

- Look for recently updated eggs.


Writing the Bug Report
----------------------

- Identify version(s) of code which manifest the bug

- Describe the symptom as clearly as possible.

- Provide a complete recipe for reproducing the bug.


Useful Patches for the Bug Report
---------------------------------

In order of increasing helpfulness:

- Changes to non-test code which work around the problem

- Unit tests which fail against the current code

- Changes to non-test code, which pass against those tests.


Bug Triage and Workflow
-----------------------

- Assigning bugs

- Prioritization

  * Bugs with patches jump the queue

- Semantics of status values

  * 'wontfix' vs. 'incomplete'

- Bugs affecting more than one project

  * Status may differ.

  * Track bug in the project whose *release* will resolve it,
    not in dependent projects (these should be "wontfix").
