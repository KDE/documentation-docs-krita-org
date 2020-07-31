.. meta::
   :description lang=en:
        Introduction to SeExpr

.. metadata-placeholder
   :authors: - L. E. Segovia <amy@amyspark.me>
   :license: GNU free documentation license 1.3 or later.

.. _seexpr_tut_intro:

Introduction to SeExpr
======================

.. versionadded:: 4.3.1

   This document will introduce you to the SeExpr expression language.

**********
Background
**********

To understand what SeExpr is about, we need to differentiate between two types
of graphics, *raster* and *procedural*.

The vast majority of the computer-generated stuff you see every day belong to
the first type-- images like photos, your favourite anime screenshots, memes,
are all a multitude of tiny little dots of color, or *pixels*, arranged into a
grid.

Raster graphics have two drawbacks. First, once you create them, their
resolution is **fixed**. You cannot zoom in and magically get any more detail.
And if you need to change them, either you go back to the source and sample it
again (which is sometimes impossible), or edit it with a raster graphics
program, like Krita.

One of the biggest problems, however, is that we are always limited by the 
**space** our programs can use; either secondary storage, like SD cards, or 
RAM. Unless compressed, image memory needs are `quadratic in the size of the 
image <https://blender.stackexchange.com/questions/112505/why-is-my-half-resolution-render-taking-a-quarter-of-the-time-of-the-full-one>`_.
For a quick example, the :ref:`create_new_document` dialog of Krita tells 
you three bits of information: its size in pixels, the size of the pixel 
itself, and *the total memory needed*.

.. image:: /images/Krita_newfile.png

Here's a summary for square textures. Note that the memory needed
is for *one layer only*:

===== ==============
Size  Memory needed
===== ==============
256   256 KB
512   1 MB
1024  4 MB
2048  16 MB
4096  64 MB
===== ==============

Procedural textures are a whole different thing. In practical terms, the only
storage needed is for its *script* - a text file of a few KB.
Load the script, and you can render your texture at whatever resolution you
need.

****************
What is SeExpr?
****************

SeExpr is an embeddable expression language, designed by Disney Animation,
that allows host applications to render dynamically generated content.
Pixar calls it `in its documentation <https://renderman.pixar.com/resources/RenderMan_20/PxrSeExpr.html>`_ a "scriptable pattern generator and
combiner".

SeExpr is available within Krita as a Fill Layer.

****************
Writing a script
****************



**************************
Creating your first preset
**************************

Once your script is ready, you can reuse it by making a preset.

You can create one through the top bar of the Options tab:

   .. image:: /images/seexpr/SeExpr_editor.png

Select :guilabel:`Save New SeExpr Preset...` and the following dialog will
open:

  .. image:: /images/seexpr/SeExpr_save.png

You can edit the name of the preset in the top line edit box, and set a  thumbnail for easy identification.

.. hint :: The dialog will append "Copy" to the preset's name if it is a copy of an existing one. You can change it at will.

The dialog provides the following choices for setting a thumbnail:

.. glossary::

   Load Existing Thumbnail
      If the preset already has a thumbnail (for instance, if you created it from an existing preset), this button will load and apply it.
   
   Load Image
      Applies an image from the filesystem as a thumbnail.
   
   Render Script to Thumbnail
      Renders your script to a 256x256 texture, and applies the latter as a thumbnail.
   
   Clear Thumbnail
      Deletes the thumbnail. Note that, if the preset is a copy of an existing one, this can be reverted by clicking :guilabel:`Load Existing Thumbnail`.

*************************
Changing existing presets
*************************

If you change a preset's script, you will notice two new buttons in the top bar of the :guilabel:`Options` tab:

   .. image:: /images/seexpr/SeExpr_overwrite_preset.png

The reload button will restore the preset to its original properties, while clicking on :guilabel:`Overwrite Preset` will save your changes.

Additionally, you can edit the preset's name by clicking on the rename button,
entering the new name, and clicking on :guilabel:`Save`:

   .. image:: /images/seexpr/SeExpr_rename_preset.png


*********************
Bundling your presets
*********************

Sharing your scripts is easy! SeExpr script presets are just like any other 
resource in Krita. Follow the instructions in :ref:`resource_management` to 
create your own bundles.
