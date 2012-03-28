Getting Off The Ground with Plone
=================================

This repository is the source for the training outline for **Getting Off The
Ground with Plone**, a modular training course aimed at beginning Plone
integrators and developers. This document is licensed under the Creative
Commons CC-BY-NC-SA License_.  You are free to re-use this material subject to
the restrictions of that license.  A copy of the license is contained in this
package under ``docs``

Building the Documentation
==========================

This documentation may be built using the tools provided by the python
docutils_ module. It uses buildout_ to create a virtualenv_, install
docutils and provide executable scripts to build each of the different 
target output types.  In order to build a particular type of documentation 
you will need to do the following::

    $ python bootstrap.py
    ...
    $ bin/buildout
    ...
    $ bin/build_s5

This will build the training module into an s5 presentation suitable for use
in a classroom setting.

Valid targets at this time include **s5** and **html**.  

.. _License: http://creativecommons.org/licenses/by-nc-sa/3.0/
.. _docutils: http://docutils.sourceforge.net/
.. _virtualenv: http://www.virtualenv.org/en/latest/index.html
.. _buildout: http://www.buildout.org/
