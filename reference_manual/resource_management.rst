.. meta::
   :description:
        Overview of Resource Management in Krita.

.. metadata-placeholder

   :authors: - Wolthera van Hövell tot Westerflier <griffinvalley@gmail.com>
             - Scott Petrovic
   :license: GNU free documentation license 1.3 or later.

.. index:: Resources, Bundles
.. _resource_management:

===================
Resource Management
===================

Resources are pluggable bits of data, like brush presets or patterns. Krita has variety of resources and also has a good resource management starting from 2.9, making it really easy for artists to share and collate all the resources together.

Bundles
-------

Starting from 2.9 Krita has a new format to manage resources it is called ''Bundles'', a bundle is just a compressed file containing all the resources together.

Tags
----

Krita also has a robust tagging system for you to manage the resources on the fly while painting. All Krita resources can be tagged. These tags can be added via the resource manager, but also via the respective dockers such as brush preset docker, pattern docker etc. You can |mouseleft| the plus icon in the docker and add a tag name. In addition to adding you can rename and delete a tag as well.

.. image:: /images/resources/Tags-krita.png
   :align: center

* Resources can belong to one or more tags.  For example, you may have a Brush Preset of a favorite **Ink Pen** variant and have it tagged so it shows in up in your Inking, Painting, Comics and Favorites groups of brushes.
* Brushes in the "Predefined" tab of the Brush Settings Editor can be also tagged and grouped for convenience.

Filtering
~~~~~~~~~


Some dockers, for example the brush preset docker as shown below, have a resource filter, which functions like a powerful search bar for the resource in question.

.. image:: /images/brushes/Brushpreset-filters.png

You can enter brush name, tag name to quickly pull up a list of brush presets you want. When you select any tag from the tag drop-down and want to include brush presets from other tags as well then you can add filters the following way: 

* To filter based on the partial, case insensitive name of the resources you can add ``partialname`` or ``!partialname``.
* To include other Tags type the respective name of the tag in square brackets like this ``[Tagname]`` or to exclude a tag type ``![Tagname]``.
* For case sensitive matching of preset name type ``"Preset name"`` or ``! "Preset name"`` to exclude.


An incredibly quick way to save a group or brushes into a tag is to:

#. Create a new tag by |mouseleft| on the green plus sign.  This will empty out the contents of the Brush Preset docker.
#. Use the :guilabel:`Resource Filter` at the bottom of the :guilabel:`Brush Presets` dock or :guilabel:`Brush Settings Editor` to type in what you want to group.  For instance: if you type **Pencil** in the filter box you will get all Brush Presets with **Pencil** somewhere in their name.  Now you have all the Pencil-related Brush Presets together in one place.
#. To finish, click the :guilabel:`Save` button (small disk icon to the right of the :guilabel:`Resource Filter` box) or press the :kbd:`Enter` key and all the items will be saved with the new tag you created.  

Now, anytime you want to open up your "digital pencil box" and see what you have to work with all you have to do is use the pull-down and select :guilabel:`Pencils`.  The Resource Filter works the same way in other parts of Krita so be on the lookout for it!

Resource Zooming
    If you find the thumbnails of the resources such as color swatches brushes and pattern to be small you can make them bigger or :guilabel:`Zoom in`. All resource selectors can be zoomed in and out of, by hovering over the selector and using the :kbd:`Ctrl +` |mousescroll| shortcut.

Managing Resources
------------------

As mentioned earlier Krita has a flexible resource management system. Starting from version 2.9 you can share various resources mentioned above by sharing a single compressed ZIP file created within Krita.

The manage resources section in the settings was also revamped for making it easy for the artists to prepare these bundle files. You can open manage resource section by going to :menuselection:`Settings --> Manage Resources...` menu item.

.. image:: /images/resources/Manageresources.png
   :align: center

Importing Bundles
~~~~~~~~~~~~~~~~~

To import a bundle click on :guilabel:`Import Bundles/Resources` button on the top right side of the dialog.
Select ``.bundle`` file format from the file type if it is not already selected, browse to the folder where you have downloaded the bundle, select it and click :guilabel:`Open`. Once the bundle is imported it will be listed in the :guilabel:`Active Bundle` section. If you don't need the bundle you can temporarily make it inactive by selecting it and clicking on the arrow button, this will move it to the :guilabel:`Inactive` section.

Creating your own Bundle
~~~~~~~~~~~~~~~~~~~~~~~~

You can create your own bundle from the resources of your choice. Click on the :guilabel:`Create bundle` button. This will open a dialog box as shown below.

.. image:: /images/resources/Creating-bundle.png

The left hand section is for filling up information about the bundle like author name, website, email, bundle icon, etc.
The right hand side provides a list of available resources. Choose the type of resource you wish to add in to the bundle from the drop-down above and add it to the bundle by selecting a resource and clicking on the arrow button.

.. warning::

    Make sure you add brush tips for used in the respective paintop presets you are adding to the bundle. If you don't provide the brush tips then the brush presets loaded from this bundle will have a 'X' mark on the thumbnail denoting that the texture is missing. And the brush preset won't be the same.

Once you have added all the resources you can create bundle by clicking on the :guilabel:`Save` button, the bundle will be saved in the location you have specified. You can then share this bundle with other artists or load it on other workstations.

Deleting Backup files
---------------------

When you delete a preset from Krita, Krita doesn't actually delete the physical copy of the preset. It just adds it to a black list so that the next time when you start Krita the presets from this list are not loaded. To delete the brushes from this list click on :guilabel:`Delete Backup Files`.

Deleting Imported Bundles
-------------------------

In case you wish to delete the bundles you have imported permanently click on the :guilabel:`Open Resource Folder` button in the :guilabel:`Manage Resources` dialog. This will open the resource folder in your file manager / explorer. Go inside the bundles folder and delete the bundle file which you don't need any more. The next time you start Krita the bundle and its associated resources will not be loaded.

Resource Types in Krita
-----------------------

.. toctree::
   :maxdepth: 1
   :glob:
   
   resource_management/*
