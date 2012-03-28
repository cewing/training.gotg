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
target output types.  

Now you have access to the docutils scripts. You can download and build the
documentation using those tools::

    (docenv)$ git clone git@github.com:cewing/training.gotg.git ./training.gotg
    ...
    (docenv)$ cd training.gotg
    (docenv)$ docenv/bin/rst2html.py source/<filename> build/<filename>

.. _License: http://creativecommons.org/licenses/by-nc-sa/3.0/
.. _docutils: http://docutils.sourceforge.net/
.. _virtualenv: http://www.virtualenv.org/en/latest/index.html
.. _buildout: http://www.buildout.org/
