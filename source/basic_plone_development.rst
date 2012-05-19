Basic Plone Development
=======================

We're going to work in this section on developing our own add-on for the Plone
system. We'll be spending a great deal more time at our command line and will
be using our text editor extensively.

.. class:: incremental

Begin by making sure that Plone (and zeo) is **not** currently running.

Plone Packages
--------------

Add-on packages for Plone tend to be categorized broadly into one of three
distinct groups:

.. class:: incremental

* Themes

  * Visual presentation, templates, css, javascript, skin layers

* Functionality

  * Content types, utilities, portlets, functional code

* Policy

  * Site setup and configuration, installation code

Why Do It This Way?
-------------------

.. class:: incremental

* Clean compartmentalization

* Minimize cross-dependencies

* Ease of re-use

* But unless you release dozens of sites, it’s a bit of overkill to be
  concerned with this

* Just put what you want into one package for now

Intro to ZopeSkel
-----------------

.. class:: incremental

* Plone is a complex system

* Add-ons require boilerplate code

* ZopeSkel helps to generate the required boilerplate so you don’t have to

What Does ZopeSkel Do?
----------------------

.. class:: incremental

* ZopeSkel provides **templates** for different types of Plone packages

* Themes, content-types (archetypes or dexterity), add-ons, policy and even
  buildouts

* None is a perfect fit for every job, you pick the template that is closest
  to what you want

Get ZopeSkel
------------

.. class:: incremental

* ZopeSkel comes with the Unified Installer and with the OS X Binary
  Installer, but not the new Windows Installer

* The version of ZopeSkel that comes is a bit old, we'll need to update it

* Those of you on Windows will need to add ZopeSkel to your buildout

Windows Users
-------------

.. class:: todo

* Open ``C:\Plone41\buildout.cfg`` in your text editor

* Add ‘zopeskel’ to the list of parts and add a ``[zopeskel]`` part at the
  end of the file

.. class:: note mini

::

    [buildout]
    ...
    parts = 
        ...
        zopeskel
    ...
    [zopeskel]
    # installs paster and ZopeSkel
    recipe = zc.recipe.egg
    eggs =
        PasteScript
        ZopeSkel==3.0a1

All Others
----------

.. class:: todo

* Open ``buildout.cfg`` from your buildout instance directory

* Find the section ``[versions]`` toward the bottom of the file

* Erase the line for ZopeSkel: ``ZopeSkel = 2.19``

* Open ''base.cfg`` from your buildout instance directory

* Find the ``[zopeskel]`` part at the end of the file

* Change ``ZopeSkel`` to ``ZopeSkel==3.0a1``

Pick Up the Changes
-------------------

We'll need to re-run buildout to pick up these changes

Windows
+++++++

::

    C:\Plone41> bin\buildout.exe

All Others
++++++++++

::

    $ bin/buildout

A Quick Word About Zopeskel
---------------------------

The version of zopeskel you have just installed is 3.0a1

* This is an early alpha of the new generation of ZopeSkel

* There are a **lot** of templates in version 2.x that are __not__ here

* If you need to use those templates, you should pin ZopeSkel's version

  * ``ZopeSkel < 3.0a1`` will do it

Learn About ZopeSkel
--------------------

Installing ZopeSkel adds a new command to your ``bin`` directory, ``zopeskel``

You can see what templates are available

.. class:: note mini

::

    C:\Plone41> bin\zopeskel.exe --list
    or
    $ bin/zopeskel --list

You can also get a full print-out of help about the tool

.. class:: note mini

::

    C:\Plone41> bin\zopeskel.exe --help
    or
    $ bin/zopeskel --help

Basic ZopeSkel Usage
-------------------- 

.. class:: incremental

* Begin creating a template using ``bin/zopeskel <template> <package.name>``

  .. class:: incremental

  * ``<template>`` is the name of the template you want to use to create your
    package

  * ``<package.name>`` is the name of the package you want to create

.. class:: incremental

* You'll first be asked if you want to answer only **Easy** questions,
  **Expert** questions, or **All** questions.

  .. class:: incremental

  * **Easy** usually enough.  Sensible defaults will be selected for the rest

Basic ZopeSkel Usage
--------------------

.. class:: incremental

* Answer the questions as they are asked.

  .. class:: incremental

  * Default values are shown in square brackets: ``[False]``

  * The answers you provide will be used to build your package

  * Your answers will be validated, so don't worry about providing the wrong
    type of information

  * If you have questions, you can type ``?`` at the prompt to get more
    information about a question

Create a Plone Package
----------------------

Windows
+++++++

::

    C:\Plone41> cd src
    C:\Plone41> ..\bin\zopeskel plone_basic my.package

All Others
++++++++++

::

    $ cd src
    $ ../bin/zopeskel plone_basic my.package

Create a Plone Package
----------------------

Provide the following answers

.. class:: note mini

::

    Expert Mode? (What ...) (easy/expert/all)?) ['easy']: <hit enter to accept the default>
    Version (Version ...) ['1.0']: <hit enter to accept the default>
    Description (One-line ...) ['']: A Package I Made
    Register Profile (Should ...) [False]: True

Extend Plone with Your Package
------------------------------

.. class:: incremental

* So far, we've only extended Plone using completed, released packages

* You can also **develop** packages using the ``develop`` configuration option
  for buildout

Developing Your Package
-----------------------

Back in ``buildout.cfg``, find the ``develop`` configuration option in the
main ``[buildout]`` part.

If it isn't there, you'll need to add it just before the second part of the
file::

    [buildout]
    ...
    develop = 
        src/my.package

Developing Your Package
-----------------------

You'll also need to add your package to the ``eggs`` configuration option for
the buildout part::

    [buildout]
    ...
    eggs =
        ...
        my.package

Picking up the Changes
----------------------

Re-run buildout to pick up the changes::

    C:\Plone41> bin\buildout.exe
    or
    $ bin/buildout

Moving Customizations
---------------------

.. class:: incremental

* Plone Wisdom says 'The custom folder is **bad**'

* This is true, *in the long run*

* But it's a great place to start working and test things out

* Eventually though, you want your changes out of there

  .. class:: incremental

  * You can put them under version control
  
  * You can share them with others
  
  * You can write tests to make sure they are working

Add Our Custom Logo
-------------------

.. class:: incremental

* To review: Plone looks for images in **skin layers**

* We need one in our package to hold our customized logo

* This requires a few steps of work

  .. class:: incremental

  1. Create a folder to be the layer container in our package
  
  2. Register this folder as a ``File System Directory``
  
  3. Register our skin in **GenericSetup**

Create a Folder
---------------

Traditionally, skin layers in a Plone package are nested inside a directory
called ``skins``

Traditionally, different types of skin elements get individual folders
(scripts, styles, images, templates)

Windows
+++++++

::

    C:\Plone41> cd my.package\src\my\package
    C:\Plone41> mkdir skins
    C:\Plone41> cd skins
    C:\Plone41> mkdir my_package_custom_images

Create a Folder
---------------

All Others
++++++++++

::

    $ cd my.package/src/my/package
    $ mkdir skins
    $ cd skins
    $ mkdir my_package_custom_images

Register the Folder with CMF
----------------------------

We use **zcml** for package-level configuration (Zope Component Meta Language)

.. class:: todo smaller

* Open ``configure.zcml`` from ``my.package/src/my/package`` in your text editor

* Add the two marked lines below (the others should already be there)

.. class:: note mini

::

    <configure
        xmlns="http://namespaces.zope.org/zope"
        xmlns:five="http://namespaces.zope.org/five"
        xmlns:i18n="http://namespaces.zope.org/i18n"
        xmlns:genericsetup="http://namespaces.zope.org/genericsetup"
        xmlns:cmf="http://namespaces.zope.org/cmf"  <<< ADD THIS LINE
        ...
      
      <five:registerPackage package="." 
        initialize=".initialize" />
      <cmf:registerDirectory             <<< AND THIS ONE
        name="my_package_custom_image"/> <<< AND THIS ONE, TOO

Register a Skin Layer with GS
-----------------------------

.. class:: incremental

* GenericSetup is a mechanism for setting site configuration

* XML files with instructions for Plone tools

* Organized into **profiles**, which contain **steps**

* Traditionally, GS goes into a folder called ``profiles`` in your package

  .. class:: incremental

  * This folder can have more than one profile, but each gets its own folder
  
  * The default profile is called ``default`` by convention

Add a GS Step For Skin Layers
-----------------------------

The Plone ``portal_skins`` tool uses GenericSetup to register new themes and
skin paths

The ``portal_skins`` GS step is called ``skins``

.. class:: todo

* Create a new file ``skins.xml`` in ``my.package/src/my/package/profiles/default``

* Open this new, empty file in your text editor and insert the following

GenericSetup for the Skin Tool
------------------------------

.. class:: note mini

::

    <?xml version="1.0"?>
    <object name="portal_skins" allow_any="False" cookie_persistence="False"
            default_skin="Club Theme">
    
      <object name="my_package_custom_images"
              meta_type="Filesystem Directory View"
              directory="my.package:skins/my_package_custom_images"/>
      
      <skin-path name="Club Theme" based-on="Sunburst Theme">
        <layer name="my_package_custom_images"
               insert-after="custom"/>
      </skin-path>
    
    </object>

Move the Custom Logo Into the Layer
-----------------------------------

.. class:: todo

* Find the 'logo.png' file in our site resources folder

* Copy that file into the new skin layer folder in your package

Activate Our New Package
------------------------

Windows
+++++++

.. class:: todo

* Start > Control Panel > System and Security > Administrative Tools >
  Services

* start ``Plone-4.1 Zeo`` (**do not start Plone-4.1**)

::

    C:\Plone41> bin\instance.exe fg

All Others
++++++++++

::

    $ bin/instance fg

Everyone
++++++++

.. class:: todo

* Go to 'Site Setup' > 'Add-ons'

* Find 'My Package' and activate it

Did it work?
------------

.. class:: incremental

* We don't actually know yet, the custom logo we added eariler is still in
  place

* Go to the 'Zope Management Interface'

* Click on 'portal_skins' and then on 'custom'

* Check the box next to 'logo.png' and delete it.

* Return to http://localhost:8080/Plone and verify that the club logo still appears

Add Our Custom Footer
---------------------

There are two ways to do this

.. class:: incremental smaller

1. The old way:

   * Register a new footer viewlet in viewlets.xml
   
   * Add a viewlet directive to configure.zcml
   
   * Add the template for the viewlet (and possibly a Python class, too)
   
   * repeat the above for each viewlet you want to override

.. class:: incremental smaller

2. The new way:
   
   * Add z3c.jbot to your package as a dependency
   
   * register an overrides directory in configure.zcml
   
   * add a template for any viewlet you want to override

z3c.jbot
--------

We are going to go with the new way

.. class:: incremental

* Allows us to override skin layer elements, browser resources, templates
  registered for views (pretty much anything you can see)

* All you need to know is the location of the original you want to override

* Great for overriding single templates when you don't want to change any
  Python functionality

* **jbot** stands for 'Just a Bunch Of Templates'

Package Dependencies
--------------------

.. class:: incremental

* Plone packages (indeed, any Python package) can **depend** on other packages

* If **a** depends on **b**, then installing **a** also installs **b**

* If your package uses code from another package, you should make the other
  package an explicit dependency.

  * If anywhere in your code you use ``from x.package import y`` then you use
    code from x.package

* This follows the basic Python principle ‘Explicit is better than Implicit’

Add a Package Dependency
------------------------

.. class:: todo

* In ``my.package`` find the file ``setup.py`` and open it in your text editor

* Find the words ``install_requires``

* Add ``z3c.jbot`` to the list of required packages

.. class:: note mini

::

    ...
    install_requires=[
        'setuptools',
        # -*- Extra requirements: -*-
        'z3c.jbot',
    ],
    ...

Set Up an Overrides Directory
-----------------------------

.. class:: todo

* Make the directory in your package

.. class:: note mini

::

    C:\Plone41> cd src\my.package\my\package
    C:\Plone41> mkdir template_overrides
    or
    $ cd src/my.package/src/my/package
    $ mkdir template_overrides

Set Up an Overrides Directory
-----------------------------

.. class:: todo

* Register the directory in my/package/configure.zcml

.. class:: note mini

::

    <!-- -*- extra stuff goes here -*- -->
    
    <include package="z3c.jbot" file="meta.zcml"/>
    <browser:templateOverrides
        directory="template_overrides"/>

.. class:: incremental

You may need to add an ``xmlns`` declaration to the top of the file. Is there
one already there for ``browser``?

Add Custom Footer Template
--------------------------

We need to know where the original template lives. To do so, we have to clear
our customized version out of the way first

.. class:: todo

* Go to 'Site Setup', then click on 'Zope Management Interface'

* Click on 'portal_view_customizations' and then click on the 'contents' tab
  at the top

* Find our customized footer and open it, copy the contents and paste them
  into an empty document in your text editor

* Return to the 'contents' tab, check the box next to our custom footer, and
  delete it.

Locating the Original Footer
----------------------------

.. class:: todo

* Click on the 'registrations' tab

* Find and then click 'plone.footer'

* Look for 'template name' in the information listed:

  * it should say ``plone.app.layout.viewlets/footer.pt``

* In ``my.package/src/my/package/template_overrides`` create a new file:

  * ``plone.app.layout.viewlets.footer.pt``

* Paste the contents of our custom footer from the empty document into this
  new file and save it.

Did That Work?
--------------

.. class:: incremental

* We don't know yet

* We have made a change to our package setup.py (added a dependency on
  z3c.jbot)

* We need to re-run buildout to pick up the change

Picking up the Changes
----------------------

.. class:: todo

* First, remember to stop plone (including the Zeo service)

* Then, re-run buildout

::

    C:\Plone41> bin\buildout.exe
    or
    $ bin/buildout

See The Results
---------------

After buildout runs, restart Plone

Windows
+++++++

.. class:: todo

* Start > Control Panel > System and Security > Administrative Tools >
  Services

* start ``Plone-4.1 Zeo`` (**do not start Plone-4.1**)

::

    C:\Plone41> bin\instance.exe fg

See The Results
---------------

After buildout runs, restart Plone

All Others
++++++++++

::

    $ bin/instance fg

.. class:: todo

* Load the front page of the site

* Do you see our new footer?

More Customizations with GS
---------------------------

Is that all the customizations we've made?

.. class:: incremental

* We also set up a site tile, right?  Way back when we first created our site?

* And we set a site description.

* We should move these out into our package, too.

Set Site Properties
-------------------

.. class:: todo

* Create a new file ``properties.xml`` in
  ``my.package/src/my/package/profiles/default``

* Open this file in your text editor

* The **properties** GenericSetup step maps onto the properties of the Plone
  site itself

* We can use it to move any changes we've made to 'Title' or 'Description'

GenericSetup for properties.xml
-------------------------------

.. class:: note mini

::

    <?xml version="1.0"?>
    <site>
      <property name="title">Happy Racquet Tennis Club</property>
      <property name="description">A great place for a great game</property>
    </site>

Control Actions
---------------

.. class:: incremental

* We discussed the dangers of the **delete** button in the folder contents
  view

* Let's Hide that action for anyone who isn't site management

* Actions are registered in Plone with a tool called 'portal_actions'

* They are organized in categories

* Like most Plone tools, they can be controlled by GenericSetup

Setting Actions
---------------

.. class:: todo

* Create a new file ``actions.xml`` in
  ``my.package/src/my/package/profiles/default``

* Open the file in your text editor and enter the following:

GenericSetup for actions.xml
----------------------------

.. class:: note mini

::

    <?xml version="1.0"?>
    <object name="portal_actions" 
            meta_type="Plone Actions Tool"
            xmlns:i18n="http://xml.zope.org/namespaces/i18n">
      <object name="folder_buttons" 
              meta_type="CMF Action Category">
        <object name="delete" 
                meta_type="CMF Action" 
                i18n:domain="plone">
          <property name="permissions">
            <element value="Manage portal"/>
          </property>
        </object>
      </object>
    </object>

Learn More
----------

We've only just begun here to scratch the surface of what GenericSetup can do.
How do you learn what else is possible?

.. class:: incremental

* Look at the profiles for other add-on packages you find, see what they do

* Look especially at the GenericSetup profiles for Products.CMFPlone
  
  .. class:: incremental
  
  * This is a treasure trove of useful lessons about what can be done with
    GenericSetup

Testing
-------

* Code changes are complicated

* Changes you make interact with changes made by others

* You need to know that your changes still work

Types of Tests
--------------

There are several different types of tests that you can write as a developer.

.. class:: incremental

* **Unit Tests** - these are the lowest-level tests, aimed at verifying that
  components of your add-ons work all on their own.

* **Doc Tests** - For a while these were in vogue as a way to test your
  package and document it all at the same time. They are losing popularity now
  and should only be written when you have no other choice

* **Integration Tests** - These tests verify that your package has
  *integrated* smoothly with the rest of the Plone system. The vast majority
  of tests you will write should fall into this category.

What to Test
------------

Opinions differ on exactly what to test in a given add-on. In general, though,
there are a few principals we can all agree on

.. class:: incremental

* Verify that your package has installed cleanly

* Verify that any components you created are present

* Verify that any skin layers you have added are present

* Verify that any changes you've made to stock settings are in effect

Writing Your First Test
-----------------------

For your first test, you will verify that your add-on package can be properly
installed

.. class:: todo

Setting up Your Tests
---------------------

There are a few changes you'll need to make to your buildout in order to be
ready to run tests

.. class:: incremental

* Add a ``[test]`` part to buildout.cfg (if you're using windows)

* Add your package to the list of packages to test (everyone)

* Re-run buildout to pick up the changes

Adding a Test Part to Buildout
------------------------------

.. class:: todo

* Open ``buildout.cfg`` in your text editor

* In the list of ``parts`` in the buildout part, add ``test`` to the end of
  the list

* At the bottom of the file, add the following code

.. class:: note mini

::

    [test]
    recipe = zc.recipe.testrunner
    defaults = ['--auto-color', '--auto-progress']

    eggs =
        my.package [test]
        ${buildout:eggs}

.. class:: todo

* Save the file

Add Your Package to Test Part
-----------------------------

Windows users, you're done with this already.

.. class:: todo

* Open the file ``develop.cfg`` in your text editor

  .. class:: smaller

  * This file contains a number of useful options for developing code
  
  * Note the in the file where it says ``extends = buildout.cfg`` (~Line 110)

.. class:: todo

* Find the line that starts with ``test-packages`` and edit it to look like
  this

.. class:: note mini

::

    test-packages =
        my.package [test]
    #    plonetheme.sunburst

* Save the file

Re-run Buildout to Pick Up Changes
----------------------------------

You have done this a bunch of times, but there's a twist this time for
non-Windows users.  Pay attention!!!

Windows
+++++++

::

    C:\Plone41> bin\buildout.exe

Re-run Buildout to Pick Up Changes
----------------------------------

All Others
++++++++++

::

    $ bin/buildout -c develop.cfg

We add this last bit to change the config file that buildout uses. Since
``develop.cfg`` extends ``buildout.cfg``, we get all of the later, plus the
former

Running Your First Test
-----------------------

Tests are of no use to anyone if they are not regularly run. Luckily, Plone
provides you with a simple way to run your tests

.. class:: todo

* Take a quick look at the ``bin`` directory in your Plone installation

* Our ``[test]`` part has added a new executable script ``test`` (on windows,
  ``test.exe``)

* We run the tests by executing that script with some options

.. class:: note mini

::

    C:\Plone41> bin\test.exe -s my.package
    or
    $ bin/test -s my.package

What you should see
-------------------

When you type the previous command, you should see a bunch of information
scrolling by. This tells you the test is working. When it finishes, you should
output like what is shown below

.. class:: note mini

::

    $ bin/test -s my.package bin/test:242: DeprecationWarning:
    zope.testing.testrunner is deprecated in favour of zope.testrunner.
    ...
      
      Running:

      Ran 1 tests with 0 failures and 0 errors in 0.011 seconds.
    Tearing down left over layers:
      Tear down my.package.testing.MyPackage:Integration in 0.000 seconds.
      Tear down my.package.testing.MyPackage in 0.003 seconds.
      Tear down plone.app.testing.layers.PloneFixture in 0.093 seconds.
      Tear down plone.testing.z2.Startup in 0.007 seconds.
      Tear down plone.testing.zca.LayerCleanup in 0.003 seconds.
    $

What Does This Mean?
--------------------

.. class:: incremental

* We have one test already written for us (thanks, ZopeSkel)

* That test is passing

* It took the test 0.011 seconds to run

  * Note that building the test environment took considerably longer

Understanding Tests in Plone
----------------------------

Testing is an important part of the development process. Let's take some time
to understand what's going on here

Open the following file from your add-on package::

    my.package/src/my/package/testing.py

.. class:: incremental

* This file contains setup code needed to create your **test fixture**

* A **test fixture** is used to set up the environment the tests will need 
  in order to run

Understanding Tests in Plone
----------------------------

.. class:: incremental

* Test fixtures consist of **layers** which are responsible for this setup

  * Our fixture starts by extending a layer called ``PLONE_FIXTURE``, imported
    from plone.app.testing

  * This layer creates an entirely new, virtual Plone site each time you run
    the tests

* Tests are written using these layers, so that the setup can be run once
  rather than having to repeat for each test you write


Understanding Tests in Plone
----------------------------

Next, open this file from your add-on package::

    my.package/src/my/package/tests/test_example.py

.. class:: incremental

* The Zope testrunner will look for any file whose name starts with ``test``

* This file will contain a test class, which extends the basic python
  ``unittest.TestCase``

Understanding Tests in Plone
----------------------------

.. class:: incremental

* This test class will have a ``layer`` attribute that points to the layer we
  set up before

  * All tests that share a layer, even from different test files, will share
    the same *environment*

  * This means that set-up takes less time. The more tests you write, the
    better your return on time invested!

* The test case will have one or more *methods* that are either tests, or code
  written to support the functionality of tests

  * Test methods will begin with ``test``

  * ``setUp`` and ``tearDown`` are magic methods that run before
    and after each test is run.

Understanding Your First Test
-----------------------------

Let's take a look at the code from the one test we have at the moment

.. class:: note mini

::

    def test_product_is_installed(self):
        """ Validate that our products GS profile has been run and the product 
            installed
        """
        pid = 'my.package'
        installed = [p['id'] for p in self.qi_tool.listInstalledProducts()]
        self.assertTrue(pid in installed,
                        'package appears not to have been installed')

.. class:: smaller

* We use the ``portal_quickinstaller`` tool, which powers the *Add-ons* 
  control panel

* We ask this tool to provide a list of installed packages and check for ours

* If it isn't there, we provide a message to let the tester know what went 
  wrong

Writing Your Own Test
---------------------

Let's add a test of our own. We've created a skin layer with our product, why
don't we verify that it is being properly added to the ``portal_skins`` tool?

Some hints:

.. class:: smaller

* The layer we added with our package is called ``my_package_custom_images``

* The ``portal_skins`` tool can be acquired during test setup just like the
  ``portal_quickinstaller`` tool was

* Layers in the skins tool are simply sub-objects of that tool.

  * Zope/Plone provides a method ``objectIds`` which returns a list of the ids
    of all the sub-objects of the object on which it is called

* When you're done, check in with me before running your tests again.

The Code for Our Second Test
----------------------------

.. class:: note mini incremental

::

    def test_skin_layer_is_added(self):
        """ verify that our product has properly added a skin layer
        """
        layer_name = 'my_package_custom_images'
        existing_layers = self.skins.objectIds()
        self.assertTrue(layer_name in existing_layers,
                        'skin layer %s has not been installed' % layer_name)

Learning More About Testing
---------------------------

Testing is a very deep pool. We've only dipped the smallest edge of our pinkie
toe into that pool. When you are ready to learn more, here are some resources:

.. class:: smaller

* The Python documentation on the unittest module
  (http://docs.python.org/library/unittest.html)

* Doug Hellman's *Python Module of the Week* post on the *unittest* module
  (http://www.doughellmann.com/PyMOTW/unittest/)

* The excellent documentation for ``plone.app.testing`` on pypi, which includes
  (http://pypi.python.org/pypi/plone.app.testing)

  * Helper functions available from the Plone Testing Fixture
    (http://pypi.python.org/pypi/plone.app.testing#helper-functions)

  * Common patterns used in writing integration tests for Plone
    (http://pypi.python.org/pypi/plone.app.testing#common-test-patterns)


