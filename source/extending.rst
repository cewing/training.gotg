Extending Plone
===============

Introduction
------------

.. class:: incremental

* Out-of-the-box Plone has an outstanding feature set

* But you often want to add more abilities, or change how plone looks

* This is done using `add-ons`

* There are many add-ons available

Introduction
------------

* You can find add-ons *both* at http://plone.org/download *and*
  http://pypi.python.org

  .. class:: incremental

  * You should check in both places, one may be more up-to-date than the 
    other

.. class:: incremental

* You can build your own add-ons, too

* Adding them to Plone is done using `Buildout`

Preparation
-----------

.. class:: incremental

* Before making **any** changes to buildout.cfg, you must **always** stop any
  systems within the buildout that are running.

* Running buildout changes executable code.

* If a system is running, and you change (or remove) the code that it uses,
  **bad things happen™**.

Stopping Plone
--------------

On Windows
++++++++++

.. class:: todo

* Stop Plone at the command prompt with ``^Z``

* Return to your services folder (did you make the shortcut?)

* Stop the **Plone-4.1 Zeo** Service

On Other Systems
++++++++++++++++

.. class:: todo

* Stop the program in your terminal with ``^C``

Add Add-ons To Your Buildout
----------------------------

To add a new package to your Plone site, you must add it to the list of 
*eggs* used in your buildout.

.. class:: todo incremental

* Open your text editor

* Open ``buildout.cfg`` from ``<installation_dir>/zinstance``

  * On Windows, this will be ``C:\Plone41\buildout.cfg``

* Find ``eggs =`` in the ``[buildout]`` part

  * add 'Products.PloneFormGen' and 'Solgema.fullcalendar' to the list

Add Add-ons To Your Buildout
----------------------------

Some add-ons require a bit of additional configuration so that Plone knows
they are present.  You point Plone to this configuration by adding the package
to the *zcml* list for your buildout

.. class:: todo incremental

* Find ``zcml =`` in the ``[buildout]`` part

  .. class:: incremental

  * add 'Solgema.fullcalendar'

  * if there is no line with 'zcml =' in your `buildout.cfg`, add one at the
    end of the [buildout] part (just before the *next* part begins)

.. class:: incremental note

**Be Aware**: capitalization counts. `Solgema` is not the same as `solgema`

What It Should Look Like
------------------------

When you're finished, the following lines should be somewhere in your
buildout.cfg file::

    [buildout] 
    ... 
    eggs = 
        ... 
        Solgema.fullcalendar
        Products.PloneFormGen
    ...
    zcml = 
        Solgema.fullcalendar

Update Your Buildout
--------------------

.. class:: incremental

* Any time you make changes to `buildout.cfg`, you need to update your
  buildout

* This is done by running the buildout script again

* As mentioned before, you only need to bootstrap your buildout once, so do
  not repeat that step when *updating*

Re-Running Buildout
-------------------

On Windows
++++++++++

You'll need to open your DOS command prompt::

    C:\> cd \Plone41
    C:\Plone41\> bin\buildout.exe

On Other Systems
----------------

In a Terminal::

    $ bin/buildout

When It's Finished
------------------

.. class:: incremental

* Executing the previous command will cause a bunch of stuff to be printed to
  the terminal window

* You should see information about the add-ons we added being found and
  downloaded

* You will see additional packages being found and downloaded

  * These are `dependencies` of our add-ons, we get them for free 

What you should see
-------------------

When it is complete, you should see something like this (although your 
numbers will differ):

.. class:: note mini

::

    *************** PICKED VERSIONS ****************
    Products.PloneFormGen = 1.7b5
    Products.PythonField = 1.1.3
    Products.TALESField = 1.1.3
    Products.TemplateFields = 1.2.5
    Solgema.fullcalendar = 1.10

    #Required by:
    #Solgema.fullcalendar 1.10
    Solgema.ContextualContentMenu = 0.1

    #Required by:
    #Products.PloneFormGen 1.7b5
    #Solgema.fullcalendar 1.10
    collective.js.jqueryui = 1.8.13.1
    *************** /PICKED VERSIONS ***************

Buildout Dangers
----------------

.. class:: incremental

* When you run buildout, it starts by *uninstalling* everything

* Buildout does not check version compatibility before it starts working

* Buildout picks the most recent version of a package by default

* This scenario can result in version conflicts

* **This is a Problem**

Defensive Buildout
------------------

.. class:: incremental

* Version conflicts are **by far** the most common problem encountered

* There is a solution

* Pin all packages to a known good version

Tools for Defense
-----------------

You can use the **buildout.dumppickedversions** extension::

    [buildout]
    extensions = buildout.dumppickedversions

.. class:: incremental

* for any package downloaded which is not pinned, it prints the selected
  version number

* You can use these picked versions to ‘pin’ your buildout

Tools for Defense
-----------------

You can alse use a configuration option for the ``[buildout]`` part::

    [buildout]
    allow-picked-versions = false

.. class:: incremental

*  buildout will quit with an error each time an unpinned egg is found
 
*  use this to iteratively pin all eggs in a buildout and make it safe

More Defenses
-------------

Some add-on packages are quite complex. Finding a complete set of their
dependencies in the correct version is not easy to do. Luckily, there's an
app(spot) for that!

http://good-py.appspot.com

.. class:: incremental

* Use [buildout] configuration 'extends' option to point to the good-py **Kown
  Good Set** (a.k.a. 'kgs') for a package

* Good-py has a list of the packages for which it has a `kgs`

* A `kgs` is specific to the version of an add-on and the version of Plone,
  check to be sure you point to the right one

Pin Your Buildout
-----------------

.. class:: todo incremental

* Find the [versions] part in your buildout.cfg

  * If your buildout doesn’t have one, add it!

* Paste the stuff that appeared in your terminal

  * everything between the two 'Picked Versions' lines (but not those lines)

  * make sure you have [versions] in your `buildout.cfg` only once!

* Save and re-run buildout

* Note that this time, there are no package versions listed at the end

Restart Plone (Windows)
-----------------------

.. class:: todo incremental

* Go to your services panel ('Start' > 'Control Panel' > 'System & Security' 
  > 'Administrative Tools' > 'Services')

* Start the **Plone-4.1 Zeo** service

* Then, at the command prompt:

.. class:: incremental

::

    C:\> cd Plone41
    C:\Plone41> bin\instance.exe fg

.. class:: note incremental

Did you save that shortcut to the services panel?  If not, do it this time.

Restart Plone (others)
----------------------

::

    $ cd <installation_dir>/zinstance
    $ bin/instance fg

Activate Our New Add-ons
------------------------

.. class:: todo incremental

* Go to http://localhost:8080/Plone

* Make sure you are logged in as 'admin'

* Click 'Site Setup' from the menu at the top right (personal tools)

* Click 'Add-Ons'

* Select 'PloneFormGen' and 'Solgema.fullcalendar' from the list of 'Available
  add-ons'

* Click 'Activate'

Behind the Scenes
-----------------

.. class:: incremental

* Look in your terminal, what do you see?

* That printed output is from `GenericSetup`

  *  It tells us about what actions were taken during activation

* Notice that more than two packages were activated

  * `GenericSetup` can automatically activate dependencies for packages

* We’ll learn more about `GenericSetup` later

Test Your Skills
----------------

You've now extended Plone with two packages that will provide add-on features.

There's one more package we want to add which will make our work easier over
the next two days. This product will prevent email from being sent out by 
Plone.  Instead, emails will be printed to the terminal.

.. class:: incremental

Let's see if you can get it done on your own!

Test Your Skills
----------------

.. class:: todo

* Stop Plone

* Add the package **Products.PrintingMailHost**

* You will *not* need to add it to the ``zcml`` list in buildout.cfg

* Re-run buildout

* Start Plone in the Foreground

.. class:: incremental note

**question**: Can you *activate* that product?

