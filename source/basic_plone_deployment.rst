Deploying Plone
===============

What we've accomplished so far
------------------------------

* Learned how to install Plone on a local machine

* Learned to extend our Plone site with add-on packages

* Learned the management of a Plone site, and customized our site settings

* Learned the basics of Plone content management, and created site content

* Learned the basics of customizing Plone through the web, and replaced some
  elements of our website

* Learned how to move our customizations to the file system, and created our
  own add-on package

What remains to be done
-----------------------

* Place our package under version control

* Learn how to set up Plone for deployment

* Learn about hosting options suitable for Plone


Version Control
---------------

Version control allows you, as a developer, to track changes to your code over
time. If you are developing code of any kind, you should be using version
control.

.. class:: incremental

* You can see how/where your code has changed

* You can annotate changes with notes about *why* the change was made

* You can *revert* changes you've made, undoing mistakes

* You can *branch* code, allowing you to work on difficult or dangerous
  changes without breaking code that already works

* You can *tag* code, freezing versions known to work for release or reference

Version Control Options
-----------------------

Version control comes in many flavors. Way back when I first started working
as a developer **CVS** was pretty much the only option. Today there are many.

.. class:: incremental

* Centralized

  * Subversion (*svn*): Venerable, solid, falling out of fashion. Requires a
    repository server somwhere 

* Distributed

  .. class:: incremental

  * Bazaar (*bzr*):

  * Mercurial (*hg*):

  * Git (*git*):

Installing Git
--------------

Git is an program that needs to be installed in your system. Luckily there are
plenty of good resources to help you do this.

Installing Git for Windows
--------------------------

A nice, binary installer is available.  Use it

.. class;: todo

* http://git-scm.com/download

* Choose the windows version and then click to download

* Run the installer, choose all default options

Installing Git for Other Systems
--------------------------------

* OS X

  * Binary version available at http://git-scm.com/download
  
  * Or you can use MacPorts

* Other Unix-like systems

  * Use your system package manager to install the package

Creating a Git Repository
-------------------------

Windows
-------

* Start up the git application from your taskbar, or the start menu

* Click **Create New Repository**

* Navigate to ``C:\Plone41\src\my.package`` and select it

Your package is now a *repository*. You may select *unstaged* files and choose
to *stage* them for commit

Once you have files *staged* you can commit them, and write a change message
to remind yourself what you've done

All Other Systems
-----------------

Once you've installed git, you should have the command available in your
$PATH.

In your terminal::

    $ cd src/my.package
    $ git init

You can add files for staging::

    $ git add <filename_or_glob>

Then you can commit those changes::

    $ git commit -m "My first commit to my new repository"

Deploying Plone
---------------

The Typical Plone Stack
-----------------------

Zope provides an HTTP server.  You've been using it.  

You do not want to put this server live online. It is not set up to operate
that way


Deploying Plone - Frontend
--------------------------

At the front end you'll want to have an http server, typically Apache or nginx

.. class:: incremental

* This will handle requests from the users, and proxy them back to Zope/Plone

* The Zope Virtual Host Monster is made to handle this case

* If your traffic is relatively light, you may not need to go farther than
  this

Deploying Plone - Backend
-------------------------

We've been running plone in *standalone* mode.  

* Zope talks directly to the ZODB

You can also run it in ZEO mode

* One or more Zope instances become clients for a *ZEO Server*

* The *ZEO Server* talks directly to the ZODB

* Allows for more active threads serving client requests up front

Deploying Plone - In-Between
----------------------------

When using a ZEO server and several Zope Clients, you'll need to have a load
balancer

* Generally a stand-alone process like **Pound** or **HAProxy**

* Can also use Apache as a load-balancer

* Helps to even out the traffic between back-end servers

Deploying Plone - Caching
-------------------------

Plone does a **lot** of work in assembling pages. If you can reduce the number
it has to build, you can speed up your site considerably

* You can use stand-alone processes like **Squid** or **Varnish**

* Apache and nginx both support caching as well

* ``plone.app.caching`` provides in-site configuration for how and when to
  cache pages

Hosting Options
---------------

* Plone is not a lightweight, $5/month hosting system

* At the very least, you'll need a hosting setup that gives you access to
  running shell commands on your server so that you can run buildout

* My personal favorite hosting service is **Web Faction**

  * You can get a small Plone site running for ~$15/month

  * There's a nice, 1-click installer that uses the UnifiedInstaller so the
    result is something you are familiar with and can update when needed

  * Most system administration is handled by professionals on their staff, so
    you can let go of that

  * Customer service is quite friendly and very fast

Other Options
-------------

* Virtual Private Server hosting

  * Rackspace, Rimu, Cloudspace

  * You'll be responsible for a *lot more* of the administration of these
    types of servers

* Cloud-based hosting

  * Amazon Web Services

    * Relatively inexpensive to set up dedicated instances

    * AMIs are available with Plone pre-loaded and set up for you, ready to go!

    * You are responsible for system and software maintenance, as with VPS
      hosting

  * Ploud.net

    * No shell access, so you're stuck with what add-ons they provide
    
    * You can customize TTW, but not with your own packages
    
    * DNS is limited to <yourinstance>.ploud.net