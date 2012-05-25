Basic Content Management
========================

The Green Frame
---------------

.. image:: ../img/green_frame.png
    :align: center
    :width: 750px

.. class:: incremental

* Daily content management activities

* Organized into tabs and menus

* Plone uses an in-place management strategy

  * The actions you take, are taken **in** the **place** where you currently
    are located


Content Creation 
----------------

Creation of content is handled through the **Add new...** menu

.. class:: incremental

* It will only show the types a user has permission to add

  .. class:: incremental

  * If you don't have permission to add anything, you won't see it

.. class:: incremental

* New types made available through add-ons automatically appear

Adding a New Page
-----------------

.. class:: todo

* Click on the ‘Add new...’ button

* Choose ‘Page’ from the menu

* Fill in a title: ``Happy Racquet Tennis Club``

* Add a description and some body text

* Make a note about what you did

* Press ‘Save’

Content Types - Classifications
-------------------------------

.. class:: incremental

* Folders

  .. class:: incremental

  * Contain other things

  * Can have ‘Default Pages’

  * Other views are available

.. class:: incremental

* Non-Folders

  .. class:: incremental

  * Do not contain other things

  * Also may have more than one view


Content Types - Frameworks
--------------------------

A content type framework is a unified set of tools providing the ability to
create different kinds of content.  A framework may also provide a basic set
of pre-defined types.

.. class:: incremental

Plone is in the midst of a transition between content type frameworks.

Content Types - Archetypes
--------------------------

The framework consists of two packages: **Products.Archetypes** and 
**Products.ATContentTypes**

.. class:: incremental

* Folder, Collection

* Page, Event, News Item, Image, File, Link

* Reliable, will be here for a while yet

Content Types - Dexterity
-------------------------

Dexterity is a re-imagining of the content type framework, aiming at being
more flexible, easier to use and more *pythonic*

.. class:: incremental

* Lightweight

* Flexible

* Can be added ‘Through The Web’

Folder Restrictions
-------------------

Plone allows the site manager to place restrictions on what types are 
available to be added, based on location.

.. class:: incremental

* Control what types of content may be added

* Provide ‘below the fold’ types

* Help guide users to do the Right Thing

.. class:: note incremental

Folderish content types may also be created with **built-in restrictions** on
what types they may contain.

Content Display 
---------------

The display of content in Plone is handled through the **Display** menu

.. class:: incremental

* If an object has more than one way to be displayed, the options will be
  found here

* You can set the **default view** for folder objects from here

  * This is identical to creating an ``index.html`` page in a static website

Change the Display
------------------

.. class:: todo

* Return to the home folder (click on ‘home’ or on the site logo)

* Click on the ‘Display’ menu

* Choose ‘Change content item as default view...’

* Select the new page you created earlier

* Press ‘Save’


Content Workflow
----------------

Content in Plone may be controlled by **workflow**. This is handled by the
**State** menu

.. class:: incremental

* Only the workflow actions you have the right to take are displayed

* Only the workflow states supported by the object are displayed

* If you have no rights to change workflow states, or there are no states
  available, this menu disappears 
  
Changing State
--------------

.. class:: todo

* Click on the ‘State’ menu

* Select Publish

* Note the new state label

Workflow
--------

* The ‘State’ Menu controls workflow

  * Shows current state

  * Drop-down menu shows available transitions

.. class:: incremental

* The ‘Advanced’ option

  .. class:: incremental

  * Set publication and expiration dates

  * Add notes about transitions

Workflow
--------

* All content items can have workflow

  .. class:: incremental

  * Not all do

.. class:: incremental

* Workflow *is* set by content type

  * We can **bind** each type to a workflow (or more than one)

* Workflow settings *can be* controlled by location (placeful workflow)

Content Overview
----------------

Access to information about all the content in a location is available via the
**Contents** tab

.. class:: incremental

* The tab only appears on folder-type objects (nothing else has contents)

* The tab is only available for someone who can *change* the contents of a
  folder

Add More Content
----------------

.. class:: todo

* While viewing the home page of your site, add a folder titled 'Court 1'

* To this new folder, add a page titled ‘Court 1’

* Add a nice, descriptive paragraph

* Provide a list of features

* Add the ‘court 1’ picture, position it at the top right

* Save and Publish the new page

Test Your Skills
----------------

Okay, you've done this one before.  Let's try it again.  

.. class:: todo

* Set the new 'Court 1' page as the default view for the 'Court 1' folder

When you've finished, click ‘Home’ in the breadcrumb navigation to go back to
the home page of your site. Then click the ‘Contents’ tab

See Quick Information
---------------------

The 'Contents' tab provides a quick look at the modification date, publication
state and size of objects.

.. class:: incremental

* Always shows all items in a folder

* Provides batch actions

  * Select more than one item with checkboxes

* Provides paged listings when there are more than 20 items in a folder

  * You can select all items then too

Change the Order
----------------

Let's move the ‘Court 1’ folder to the top

.. class:: todo

* Click and hold the ‘handle’ at the left

* Drag the row to the top

* Release mouse button

* Note that the position of the 'Court 1' tab at the top of the site changes,
  too

Duplicating Content
-------------------

The **Contents** tab offers more than just information and ordering

.. class:: todo

* Check the box next to the 'Court 1' folder

* Below the table of content, click the **copy** button

* Once your page has fully reloaded, click the **paste** button that has just
  appeared

You should now have a *second* 'Court 1' folder listed at the bottom of the
table

Advanced Workflow Control
-------------------------

.. class:: incremental

* Note that the new folder is 'private'

  * The page inside it is, too
  
  * This is the *initial state* of the default workflow
  
* We can change both at once 

* We can also set 'publish' and 'pull' dates for our content

* And we can make notes about the changes we make to workflow, just like those
  we can make when creating or editing content

* We need to use the **Change State** action

Change State
------------

.. class:: todo

* Check the box next to the new, private 'Court 1' folder

* Click the **Change State** button below the contents table

* In the form that opens, check ``Include contained items``

* Make a note in the ``Comments`` field about what you're doing, and why

* Click the button for ``Publish`` at the bottom

* Click **Save**

* Check to see that the page inside this folder has also been published

Controlling Names
-----------------

.. class:: incremental

* Plone content ids (the bit that shows in the URL) are generated 
  automatically from the title

* This can lead to unwieldy URLs for your content

* Copied content gets an id identical to the original, with 'copy_of'
  prepended

* You can change this with the **Rename** button.

Rename Our Copy
---------------

.. class:: todo

* Back in the **Contents** tab for the home page, check the box next to the
  *copied* 'Court 1' folder

* Click on the **Rename** button below the content table

* In the form that opens, enter these values

  * **New Short Name**: ``court-2``
  
  * **New Title**: ``Court 2``

* Click Save

Deleting Content
----------------

.. class:: incremental

* There are two ways to get rid of content in Plone.  

  1. Use the **Actions** menu on a content item to delete it.
  
  2. Use the **Delete** button from the **Contents** tab

* The former only works on one item at a time (although if you delete a
  folder, all the stuff in it is gone too)

* The latter works on batches of content

Delete the News Folder
----------------------

.. class:: todo

* Click on the 'News' tab at the top of your site, so you are viewing the 
  news aggregator

* Click on the 'Contents' tab of the green frame to ensure we are viewing the
  'news' folder

* Click on the **Actions** drop-down menu and select **Delete**

* When the confirmation dialog appears, decide if you want to actually do 
  this.

Delete the Original Home Page
-----------------------------

.. class:: todo

* Return to the contents tab of the home of your site

* Check the box next to ``Welcome to Plone``

* Click **Delete** below the contents table

Did you notice that there was **no** dialog to confirm that you wanted to do
this? The **Actions** menu method *did* have a confirm dialog.

Content Editing
---------------

Access to editing a piece of content is handled through the **Edit** tab

Editing Content
---------------

.. class:: todo

* Click on the name of the 'Court 2' folder to see the contents view of that
  folder 

* Click on the name of the ‘Court 2’ page

* Click on the ‘Edit’ tab

* Change the text to fit the new court

  * **Make sure to add a couple of paragraphs and a sub-heading or two**

* Replace the image with the ‘Court 2’ image

* Make a note about the change

* Press ‘Save’

Editing 'Metadata'
------------------

.. class:: todo

* Click the ‘Edit’ tab again

* Click the ‘Categorization’ sub-tab

  * Add keywords, build relationships between content, geocode your content

* Click the ‘Dates’ sub-tab

  * Set publication and expiration dates
  
  * These are the same as in the **Change State** form

* Click the ‘Ownership’ sub-tab

  * Set rights, contributors and creators

  * This is strictly informative, no effect on access

Edit Settings
-------------

.. class:: todo

* Click the ‘Settings’ sub-tab

* Select ‘table of contents’

* Make a note of the changes you’ve made

* Press ‘Save’

* Note a table of contents has been created (assuming you added sub-headings
  when you edited the page)

Versioning Content
------------------

.. class:: incremental

* Plone automatically keeps older versions of your content

* You can view old versions

* You can compare versions to see what changed

* You can revert to any version and return

View History
------------

.. class:: todo

* Edit the page a few more times, making minor changes.  

  * Add change notes each time

* Click ‘history’, next to the by-line, below the title

  * Notice how helpful your change notes are

* Click ‘compare’ between two versions

  * Check out the difference between *inline* and *code*

* Click ‘revert to this version’ on an earlier version

.. class:: note incremental

Note that reverting simply adds a new entry to the history, so you can
‘revert’ back to a later version

Content Access
--------------

The rights that users and groups have in relationship to a piece of content or
even a whole folder can be controlled locally using the **Sharing** tab

Understanding Plone Access Control
----------------------------------

.. class:: incremental

* Workflow in Plone is based on:

* **Permissions** and **Roles**

* **Users** and **Groups**

* Workflow States control which **permissions** are granted to which **roles**

* Sharing controls which **roles** are granted to which **users** and
  **groups**, *locally*

Standard Plone Roles
--------------------

.. class:: incremental

* Sharable:

  .. class:: incremental

  * Reader—Can view things

  * Contributor—Can add things

  * Reviewer—Can change state of things

  * Editor—Can modify things

.. class:: incremental

* Not Sharable:

  .. class:: incremental

  * Owner—Given to the user who creates a thing

  * Site Administrator—Controls the whole Plone site

  * Manager—Controls the entire Zope Instance

Sharing Private Content
-----------------------

.. class:: todo

* Retract both ‘Court 1’ and ‘Court 2’ to the private state

  * Use the **Change State** button to do this, so you get everything at once

* View ‘Court 1’

* Click on the ‘Sharing’ tab

* Check the box in the ‘Can View’ column for ‘Logged-in users’

* Press ‘Save’

Check Your Work
---------------

.. class:: todo

* Return to your browser tab with 127.0.0.1 open

* Log in as ``jmember`` (password ‘secret’)

* Note that you can see ‘Court 1’ but not ‘Court 2’

What's Happening Here?
----------------------

* ``jmember`` is a member of the group ‘logged-in users’

* We shared the right to *view* with that group **locally** for Court 1

* This allows ``jmember`` to view that one piece of private content, but not the
  other.

Grant a Global Role
-------------------

Return to the tab showing ‘localhost:8080’

.. class:: todo

* Click ‘Users and Groups’

* Find Joe Member in the list of users (you may have to use search)
   
* Check the box in the ‘Reader’ column

* Press ‘Apply Changes’

Check Your Work
---------------

.. class:: todo

* Return to the 127.0.0.1:8080 tab where you are logged in as ``jmember``

* Reload your page

* Note that you can now see ‘Court 2’

What's Happening Here?
----------------------

**Global Roles** apply across the entire site, regardless of what’s in the
sharing tab

.. class:: todo

* Return to the localhost:8080 tab

* Revoke the global role of ‘Reader’ for Joe

* Re-publish both 'Court 1' and 'Court 2' so that visitors can see them

Collections
-----------

.. class:: incremental

* A special content type, very powerful

* Looks like a folder, but is not, really

* You set **criteria**, which are used in an automated **search**

* The results of the search are displayed as if they were contained in the
  collection

* You can search using *type*, *state*, *location*, *keyword* and much, much
  more

* A great way to build automated aggregators of content for display

Reservation Calendar
--------------------

Let's use the power of Collections to build a simple reservation calendar for
'Court 1'

.. class:: todo

* Go to the 'Court 1' folder and add a new Folder called ``Reservations``

* Inside that folder, add a new **Collection**

* Give it the title ``Court 1 Reservations``

* Give it a description: ``See when the court is being used. Make your own
  reservations.``

* Save your new Collection

Setting Criteria
----------------

At the moment, nothing shows in our collection because we have yet to tell it
what to search for. We need to fix that by adding criteria.  Doing so is a 
two-step process.

.. class:: incremental

1. Add a new criterion

   * Choose the type of information to search for
   
   * Choose the way you will provide specific information for the search

2. Edit the settings for the criterion

   * Provide the specific information for the search

Add Criteria For Reservations (I)
---------------------------------

.. class:: todo

* Click on the **Criteria** tab in the green frame

* Under *Add New Search Criteria*, in ``Field Name`` select ``Item Type``

  * This criterion allows us to search for content items of a particular type
  
  * Our reservations will be **Events**
  
* In ``Criteria Type`` leave the value ``Select content types``

* Click **Add criteria** at the bottom of this form section

Add Criteria For Reservations (II)
----------------------------------

.. class:: todo

* Once the page reloads, select *Event* from the list of content types

* Leave the ``operator name`` as ``or``

  * The ``operator`` determines how you combine more than one value *within a
    single criterion*

  * Multiple criteria are always combined with **and**

* Press **Save**

Add Another Criterion
---------------------

Now our collection will show events. But it will show *all* events,
everywhere.  We want to further restrict our search

.. class:: todo smaller

* In the *Add New Search Criteria* section, select the ``Field Name``
  ``Location``

  * This will allow us to search for items in a particular *place*

* In ``Criteria Type``, select ``Location in site relative to current location``

* Click **Add criteria** at the bottom of this form section

* When the page reloads, find our new criterion in the list of criteria and
  note the current value.  It's appropriate, so press **Save**

Set Appropriate Rights 
----------------------

Now our Collection will show only events that are added to the 'Court 1
Reservations` Folder. We need to allow logged-in users of our site to add new
reservations.

.. class:: todo

* Move one level up so that you are looking at the 'Reservations'
  folder

* Click on the **Sharing** tab to set permissions for this folder

* Check the box under ``Can add`` for ``Logged-in users``

* Click **Save** to preserve our changes

Add Some Reservations
---------------------

Okay, now you've done the hard part. It's time to have a bit of fun. Add a few
**Events** to the 'Court 1 Reservations` folder. In between adding them, view
your **Collection** and see how they start to appear as you create them.

Test Your Skills
----------------

Our system is pretty good, but it could certainly be better. Take a few
moments to practice what you've learned so far by making the following
improvements to the reservations system:

.. class:: todo smaller

* Our collection currently shows all events in the reservations folder. Change
  it to show only ``published`` events

* Our users can add any type of content to our reservations folder.  Set up
  content restrictions so that only *events* may be added.

* The collection is not very good looking. And it's hard to read as a
  calendar. Change the display of the collection so that is uses the
  ``fullcalendar view``

* Our reservations folder currently lists the collection. It'd be nice to see
  the collection immediately upon coming to the folder. Make the collection
  the default view for the folder
