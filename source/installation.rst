Installation and Setup
======================

Download Plone
--------------

.. class:: todo

* Open your web browser

* Go to http://plone.org

* Click on ‘Download & Extend’

* Click on ‘Download Plone’

* Select an appropriate installer

  .. class:: info

  * For Windows, the Windows Installer

  * For Unix/Linux, the Unified Installer

  * For OS X, the OS X installer or the Unified Installer
    
.. class:: incremental note

OS X Lion has a special binary installer.  It is *not* the same as earlier versions

Install Plone
-------------

.. class:: incremental

* Plone is best installed using one of the installers

* You can also manually install it, once you've learned enough to do so

* We will use one of the installers today

Installer Notes
---------------

.. class:: incremental

* All Installers contain everything you need

  .. class:: incremental

  * This means once you have the installer, you *can* run it without a network
    connection

* The Unified Installer **requires** that you have a compiler for the
  **C** programming language installed on your machine

Binary Installers
-----------------

.. class:: todo incremental

* Save the installer to your desktop

* Run the installer:

  * Windows:  double-click installer file

    * Installed code at C:\Plone41

  * OS X:  double-click installer file

    * Choose a type (standalone)

    * Choose a password (‘admin’)

    * Installed code at /Applications/Plone

Unified Installer
-----------------

.. class:: todo

* Unpack the Unified Installer

::

    $ tar -zxvf <installer_tarball>

.. class:: todo

* Run the installation script

::

    $ cd <installer_directory>
    $ ./install.sh --target=<path> --password=admin standalone

.. class:: incremental

Installed code at <path>

.. class:: incremental

Lots more information in README.txt


Starting Plone
--------------

Plone can be started in two ways

.. class:: incremental

* Daemon mode

  .. class:: incremental

  * Used for production

  * Program output is sent to log files

.. class:: incremental

* In the foreground 

  .. class:: incremental

  * Good for development

  * Program output is sent to the terminal where the system is running

    * You can see what is happening, as it happens

  * This is how we'll do it for the duration of this class
  
    * You should always do it this way when you're developing at home, too

Start Plone in the Foreground
-----------------------------

Windows:
++++++++

.. class:: todo

* Open 'Start' > 'Control Panel' > 'System and Security' (in Win7,
  others may skip this) > 'Administrative Tools' > Services

* Find the 'Plone-4.1 Zeo ' service, make sure it is started.

* Find the 'Plone-4.1' service, make sure it is __not__ started.

* Open your command prompt

::

    C:\> cd Plone41
    C:\Plone41> bin\instance.exe fg

.. class:: incremental note

If you get an error asking you to stop the instance first, find and delete
C:\Plone41\var\instance.pid and C:\Plone41\var\instance.lock

.. class:: incremental note

You may wish to make a shortcut to the `Services` panel on your desktop to
save time. We'll be in there quite often

Start Plone in the Foreground
-----------------------------

All Others:
+++++++++++

::

    $ cd <installation_dir>/zinstance
    $ bin/instance fg

Create Your First Site
----------------------

.. class:: todo incremental

* Open your web browser

* Go to http://localhost:8080/

* Click 'Create a new Plone site'

* Provide the Username and Password

  * If you've been following along: *admin* and *admin*

* Use the following settings:

  * **Path identifier**: 'Plone'
  * **Title**: 'Happy Racquet Tennis Club'
  * **Site language**: 'English'

* **Do not** select any add-ons for installation

* Click 'Create site'


Behind the Scenes
-----------------

Why the different installation methods?

.. class:: incremental 

* Actually, the methods are only different on the surface

* Underneath, all are based on `zc.buildout` (a.k.a. `Buildout`)

* This means that once we've finished running the installer, we are
  all working from the same environment.

* This simplifies the process of development across different 
  platforms

Buildout Basics
---------------

.. class:: incremental 

* A system for controlling the distribution and deployment of complex
  software environments

* Easy to get started working

  .. class:: incremental 

  * Only requires two files:

    .. class:: incremental 

    * `bootstrap.py` (you **never** edit this)

    * `buildout.cfg` (your configuration goes here)

      .. class:: incremental 

      * Uses the familiar 'ini-style' format

.. class:: incremental 

* Flexible and powerful

* Based on **parts**, **recipes**, and **configuration data**


Parts
-----

* Parts represent functional units of configuration

.. class:: incremental

* Parts are designated by square brackets around a name

  * All buildouts require at least the [buildout] part

  * Global configuration can be set in this part

* Parts may have a recipe 

  * This will be designated on the line immediately after the part name

Parts
-----

* Parts will have configuration data

.. class:: incremental

* The [buildout] part will have a list of the other parts that will be run::
    
    parts = 
       <part_1>
       <part_2>
       ...
       <part_N>

Recipes
-------

.. class:: incremental 

* Recipes are sets of Python code that know how to perform a given task

* Recipes control the building of sub-systems within your environment

  .. class:: incremental 

  * install a python egg

  * set up a zope instance

  * install software using the cmmi pattern

  * and much more ...

.. class:: incremental 

* Each recipe has a list of configuration options available

* You can find recipes, and read about the options for ones you've found
  at http://pypi.python.org

Configuration Data
------------------

.. class:: incremental 

* Each part in a buildout will have some

* Options take the form <option_name> = <value>

  .. class:: incremental 

  * can also be a list of values for some options

.. class:: incremental 

::

    <option_name> = 
        <value_1>
        <value_2>
        ...
        <value_N>

Using Buildout
--------------

.. class:: incremental 

* A buildout will consist of a folder with at least the two required files

* Executing the set-up instructions represented by a buildout is called
  *running the buildout*

* It is a two-step process

  .. class:: incremental 

  1. Bootstrap the buildout
  
  2. Run the buildout

Bootstrapping a Buildout
------------------------

.. class:: incremental 

* This creates the buildout script, with a hard-coded reference 
  to the python used to run the command

* The script is placed in a `bin` directory created in the same folder
  as `buildout.cfg`

* This step need only be done once (the first time)

Running a Buildout
------------------

* This executes each of the recipes in your buildout parts in turn

  * If a part introduces a dependency on another part, they may be run out of
    order 

* Required packages are downloaded or located on your local machine

::

        $ cd <buildout_directory>
        $ /path/to/python bootstrap.py
        ... (a lot of output will happen here)
        $ bin/buildout

.. class:: incremental

* When it's over, you have a system in place that will be identical to that of
  anyone else who has run the same buildout
