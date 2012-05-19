Tour of Plone
=============

A Quick tour of A Plone Site
----------------------------

Plone creates a number of consistent structures that all Plone sites share in
common. Some may have been removed, or changed in position, but they are always
*available* to the site designer.

Page Structure
--------------

The Site Header
+++++++++++++++

.. image:: ../img/plone_header.png
    :align: center
    :width: 600px

.. class:: incremental smaller

* Contains the logo, search bar and global navigation tabs

* Usually contains the log in and log out UI, and access to member data

Page Structure
--------------

The Site Footer
+++++++++++++++

.. image:: ../img/plone_footer.png
    :align: center
    :width: 600px

.. class:: incremental smaller

* Contains site-wide actions like contact and site map

* Generally contains colophon about the site

Page Structure
--------------

The Site Body
+++++++++++++

.. image:: ../img/plone_body.png
    :align: center
    :width: 600px

.. class:: incremental smaller

* The **editable** part of a site

* The appearance of this will change depending on the type of content being
  shown

Page Structure
--------------

The Site Portlet Columns
++++++++++++++++++++++++

.. image:: ../img/plone_columns.png
    :align: center
    :width: 600px

.. class:: incremental smaller

* Dynamic content contained in portlets

* What is shown can depend both on who and where you are

* If there is no content to show, the entire column will be omitted

Page Structure
--------------

The ‘Green Frame’
+++++++++++++++++

.. image:: ../img/green_frame.png
    :align: center
    :width: 600px

.. class:: incremental smaller

* The main UI for editing and managing content in Plone

* Organized into *Tabs* and *Menus*

* Users will only see what they can use


Features of Plone
-----------------

.. class:: incremental

* In-place editing

  * Where you create something is where you find it

* Simple, configurable user interface

  * You control what the user can do and where

* Highly customizable site settings

  * All settings in one convenient place, **Site Setup**



Tour Site Setup
---------------

.. class:: incremental

* You’ve already been here once, to activate your new add-ons

* You can control pretty much everything about your site as a whole from here

* Only available to `Managers` and (since Plone 4) `Site Administrators`


Security
--------

Controls aspects of site-wide access

.. class:: incremental

* Self Registration (can people join?)

* Choose Own Password (or email link)

* User Folders (automatically give them a place to create content?)

* ‘About’ information (are by-lines public?)

* Email address as login (or create one)

Our Class Settings
------------------

.. class:: todo

* Select ‘Enable self-registration’

* Select ‘Let user select their own passwords’

  * This is for testing only.  I would not do this on a live site

* Press ‘Save’


Register a New User
-------------------

.. class:: todo

* Open a new tab in your browser

* Enter the url http://127.0.0.1:8080/Plone

* Click the ‘Register’ button at the top right

* Full Name: ``Joe Member``

* User Name: ``jmember``

* Email: just make sure it's a *valid* one

* Password: ``secret``

* Press ‘Register’

Users and Groups
----------------

Controls all aspects of User and Group management

.. class:: incremental

* Add users and groups manually

* Place users in groups or remove them

* Control what is available on dashboards

* Grant users and groups **global** roles

* Control settings for user/group display

  * If you expect lots of users or groups, check the boxes

* Choose what information is asked for at registration time


View the New User
-----------------

.. class:: todo

* Return to the tab showing ‘localhost:8080’

* Click ‘Users and Groups’

* Find Joe Member in the list of users

* If you checked ‘many users’, you’ll have to search to see him

* Note that he is automatically granted the `Member` global role.


Add-Ons
-------

Controls which products are activated in your site

.. class:: incremental

* Allows you to upgrade products that have new versions downloaded

  * Some older products may have an ‘error’ message about ‘no upgrade
    available’, you can safely ignore this.

* You can also deactivate add-ons

  * Always test this.  Some products leave stuff behind


Activate Another Add-On
-----------------------

You’ve done this before.  Let’s do it again

.. class:: todo

* Activate ‘Working Copy Support’

* Note the information in your terminal


Errors
------

Information about anything that goes wrong in your site can be found here

.. class:: incremental smaller

* When your users have problems, look here

* Be aware of ‘ignored exception types’

  * If you have misconfigured permissions, ignoring ‘Unauthorized’ is not a
    good idea.

  .. class:: incremental

  * You will see debugging references to ‘removing ignored exception types’.
    This is where you do it

.. class:: incremental smaller

* Be aware on Zeo installations, errors shown for only one client at a time

  * You may need to reload the page multiple times before you hit the right
    client and can see your error


Mail
----

.. class:: incremental

* Controls the mail connection from your site to the outside world

* Much of plone’s functionality will not work without this

  * Contact form, mail to authors, content rules, self-registration w/out
    password


Set Up Mail
-----------

We've installed **Products.PrintingMailHost** so most of this is simply for
information. You will need to set the site **From Address**

* SMTP Mail Host: <a good smtp mail server>

* SMTP Port: (25 is standard)

* ESMTP username: <if required>

* ESMTP password: <if required>

* From Name: <Your name>

.. class:: todo

* From Address: <your email address>

* Press ‘Save’

Navigation
----------

Controls the behavior of Plone’s built-in navigation system

.. class:: incremental

* Can replace automatically generated tabs

* Can make only folders show as tabs

* Can choose to ignore certain content types entirely (like images, perhaps?)

* Can also exclude items based on workflow

Our Navigation Settings
-----------------------

.. class:: todo

* Set the navigation system to only show folders as tabs

* Set the system to ignore ``Images``, ``Files``, ``Events`` and ``News
  Items``


Site
----

Controls how your site presents itself to the outside world.

.. class:: incremental

* Site Name will appear in <title> tag for all pages

* Site Description will appear in search engines

* You can achieve pretty good SEO by enabling Dublin Core Metadata (assuming
  you use keywords and dates and such)

* Javascript for Web Statistics support can be very powerful.

  * Especially combined with `collective.googleanalytics`

Our Site Settings
-----------------

.. class:: todo

* Set the description to ``A great place for a great game``

Theme
-----

Control aspects of how your site appears to the outside world

.. class:: incremental

* Choose which of the installed themes is currently being used

  * Theme products must be active to show

* Choose to whom you show content type icons

* Choose whether to use pop-up overlays for forms


Activate a Theme
----------------

.. class:: todo

* Choose ‘Plone Classic Theme’ from the drop-down

* Press ‘Save’

* Note the difference

.. class:: todo incremental

* Do it again with ‘Unstyled’

  * This is your site without **any** CSS!

* And return to ‘Sunburst’
