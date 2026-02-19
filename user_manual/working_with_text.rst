.. meta::
   :description property=og\:description:
        Introduction to using the text tools in Krita.

.. metadata-placeholder

   :authors: - Wolthera van Hövell tot Westerflier <griffinvalley@gmail.com>
   :license: GNU free documentation license 1.3 or later.

.. index:: Text

.. _working_with_text:

====================
 Working with Text
====================

Krita has a number of features for creating and editing text. While basic use is straightforward, there's a number of advanced features that make working with text really fast. This chapter will give an overview of how the different parts work together.

Overview
--------

The main tool for text is the :ref:`text_tool`, which allows you to create text objects. It also allows you to edit ranges of text, that is, typing, copying and pasting text. But also setting the font, color and size on a range, and even more advanced type setting, like selecting glyph alternates and precise positioning of glyphs.

The Text Tool is used together with the :ref:`text_properties_docker`, which gives you full control over all text properties. It also has :ref:`resource_style_presets` to make it easy to reuse certain property combinations.

However, the Text Tool can only edit a single text at a time. To edit multiple texts, you can use the :ref:`shape_selection_tool`. The text properties docker will edit all selected text objects when using the Shape Selection Tool. Similarly, the Shape Selection Tool can be used to set text on path, or put text into multiple shapes.

To show how these tools are used together, lets go over some examples:

Creating A Decorative Header
----------------------------

Say you want to add some text to an illustration, like you would do for a poster or greeting card.

Select the :ref:`text_tool` and |mouseleft| the canvas to create a new text. You can now type your text.

.. figure:: /images/text/working_text_decorative_1.png

To adjust the colors and stroke, you can select a color directly from any of Krita's color pickers. For the font and text size however, you will need to use the :ref:`text_properties_docker`.

.. figure:: /images/text/working_text_decorative_2.png

In the Text Properties Docker, the :guilabel:`Paragraph` tab will change the properties over the whole text, while the :guilabel:`Character` tab will only change properties for the current selection.



When you have changed a property in the character tab, the button on the left will be activated. Pressing it will undo the change, but it being active also tells you which properties are set on characters. Properties that are set on the characters won't be affected by the properties set on the paragraph. 

.. figure:: /images/text/working_text_decorative_3.png

   Here we added an underline in the :guilabel:`Character` tab.

For example, lets underline this bit of text. Select the text. Then go to the :guilabel:`Character` tab and to :guilabel:`Add Property` at the bottom, and type "underline". You will see :guilabel:`Text Decoration` in the list. Select this. Now, toggle :guilabel:`Underline`.

.. figure:: /images/text/working_text_decorative_4.png

   Here, we went back to the :guilabel:`Paragraph` tab, and only changed the font family.

Now when you go back to the :guilabel:`Paragraph` tab, and adjust the font, the underline is kept on our original selection.

.. figure:: /images/text/working_text_decorative_5.png

   Same as above. Each of these samples uses a different font, but because this is only adjusted on the :guilabel:`Paragraph` tab, the underline, which was set in the :guilabel:`Character` tab is left alone.

This can be used with any of the :ref:`text_character_properties`, and can be used to keep consistency in a text while still being able to style each character individually.

Using Glyph Alternates
~~~~~~~~~~~~~~~~~~~~~~

Some fonts have alternate :term:`glyphs` for specific characters for decorative effects. To access them, you can use the :ref:`text_property_open_type` in the text properties docker, but it is more convenient to use the :ref:`glyph_palette`.

To open the glyph palette, go to the Text Tool options, and press :guilabel:`Glyph Palette`.

.. figure:: /images/text/working_text_palette.png

If there's a text active, and the font supports glyph alternates for the given glyph, it will be show in the palette.

Double click an alternate glyph to select it.

Curving And Per-Character Positioning
-------------------------------------

Sometimes you want to have more control over the position of the :term:`glyphs`. You can do this with the :ref:`type_setting_mode` in the Text Tool options. First ensure that the text is preformatted by selecting :guilabel:`Preformatted` in the Text Tool options. Then, click the :guilabel:`Type Setting Mode` button to enable it.

.. figure:: /images/text/working_text_adjust_typeset_mode_1.png

.. figure:: /images/text/working_text_adjust_typeset_mode_2.png

The selection area on canvas will now have been replaced with a series of lines. And two dots will be at the start and end of the selection area. You can |mouseleft| + drag the dots to move the whole selection.

.. figure:: /images/text/working_text_adjust_typeset_mode_3.png

While this is powerful, sometimes you want to have the whole text follow a path without having to adjust every character individually.

To do so, first, create a path on a vector layer.

.. figure:: /images/text/working_text_adjust_path.png

Then hover over the path with the :ref:`text_tool`, and press |mouseleft|.

.. figure:: /images/text/working_text_adjust_path_2.png

You will now be able to adjust the text postion on the path, and with the :ref:`shape_edit_tool` you can adjust the path. You will first need to go into contour mode (the top right icon) and then select and edit the path as usual.

To hide the path, use the :ref:`shape_selection_tool` to select it and set the opacity to 0%.

.. figure:: /images/text/working_text_to_path.png

Finally, if these two functions don't do what you need them to do, there's always :guilabel:`Convert to Path` in the :ref:`shape_edit_tool` options. Clicking this will convert the text into a regular vector shape (if you have multiple colors in use, it will produce a group shape, so you will need to ungroup with the :ref:`shape_selection_tool` context menu).

Comics
------

When creating a comic, you can add text at any given moment. The examples here focus on the most common moments: At the very start, when planning a comic, or at the very end, when type setting a comic.

Now, when creating a comic, it is important that the text is consistent and and easy to read. To ensure that, you can use :ref:`resource_style_presets`. First, create a text. Then, with the :ref:`text_properties_docker`, set the preferred font, and the font size. Finally, create a style preset by going to the :guilabel:`Preset` tab, and there selecting :guilabel:`New Preset`. A dialog will pop up, where you can set the name and the style sample.

.. figure:: /images/text/working_text_comics_preset.png

Now, you can go into the tool options for the Text Tool, and untick :guilabel:`Current Text Properties`, then select your new preset in the dropdown. New texts will now be created with that preset, making it easy to keep everything consistent.

.. tip::

    It can be tricky to determine a readable font size, as images on screen are bigger or smaller than their printed outputs depending on the screen. This is because programs like Krita display images so that at 100% a single pixel in the image is a single pixel on the screen. But it is possible to switch to physical size too. There's a button next to the zoom slider at the bottom that allows you to switch between pixel sizing and physical sizing. When switched to physical sizing, Krita will display the image zoomed to its physical size at 100%.
    
    To determine a readable font size, you then create a text with your preferred font. Then switch to physical size. If you work at twice the physical size, you will need to zoom to 50%, if not, zoom to 100%. Then, sit at an arms' length from the monitor, and adjust the font size of the text until it is pleasant to read.
    
    If you don't work for print, you can skip the physical zoom step, and instead adjust the zoom so that it is the same size on screen as the end result. Then adjust the font size as necessary.

Planning A Comic
~~~~~~~~~~~~~~~~

Methods that put text onto a comic at the very start do so because the artist wants to make sure that the text has enough room, and they plan the images around the text.

Now, you might be working off a script or a very rough sketch. The first thing you do then is create new texts. You can do this with the :ref:`text_tool`, by doing |mouseleft| + drag a large rectangle to create a :ref:`text_inline_wrapped` area. Then type your text. This inline-wrapped length is useful here because it doesn't cut off at any given point, so you can focus on typing text and adjusting it afterwards.

You can use the :ref:`shape_selection_tool` to select multiple text shapes and adjust them with the :ref:`text_properties_docker`. This will only affect the :guilabel:`Paragraph` level properties.

.. figure:: /images/text/working_text_planning_comics.png

   With all the texts in place, this comic page is ready to be pencilled. By having the texts laid out like this, it becomes straightforward to see how much space there is left for the images.

Type Setting A Comic
~~~~~~~~~~~~~~~~~~~~

The other method of putting text on comics is at the very end, after all colors and images are finished. This is usually referred to as "Type Setting" a comic, as it is not just about putting the text in place, but also making it look good together with the images.

Now, all the previous examples already showed how we can make the kind of decorative text for titles and onomatopoeia. For this section, we'll be focusing on flowing text directly into a balloon.

.. figure:: /images/text/working_text_typeset_comics_1.png

   Image (and later example text) courtesy of Pepper and Carrot, CC-BY David Revoy

First, create a closed shape on a vector layer.

.. figure:: /images/text/working_text_typeset_comics_2.png

Then hover over the center with the :ref:`text_tool` and |mouseleft|.

You can now type the text.

.. figure:: /images/text/working_text_typeset_comics_3.png

If you want to add some padding, hover over the border of the shape, and |mouseleft| + drag inwards to add some padding.

An alternative manner of putting text in a shape is to create a text, and a shape for it to flow in. Then, with the :ref:`shape_selection_tool` select both, and |mouseright| for the context menu. There, select :menuselection:`Text --> Flow Text in Shape`. If you have multiple shapes selected, you can flow the text into multiple shapes as well.

When you have a text in shape, you can adjust it's size by resizing with the shape selection tool, but you can also switch into contour mode (by clicking the new button at the top right) to move the shapes individually.


Text Term Glossary
------------------

There's a number of technical terms that are used throughout the manual to describe certain functionality. These technical terms are so common that it is easier to provide a glossary of their meanings than to explain them every time their come up.

.. glossary::

    Characters
        This refers to individual letters in a text. "Individual" is doing a lot of heavy lifting here, as not all languages have unique letters, but instead use clusters of letters that get represented by a single glyph. In any case, within the documentation we'll be using character to refer to the text as it is typed, and glyph to refer to the pictures that make up the text.
        
    Glyphs
        This is the name of the image or vector shape that represents a character or cluster of characters. The glyph selected is determined by the font, language and any OpenType features that are enabled.
        
    OpenType
        Fonts are not just collections of glyphs for each character and cluster, but also contain a tiny program that instructs the text layout how to use the glyphs. OpenType is a standard for these programs, and Krita allows you to configure the features of the program via various OpenType feature controls.
        
    Advance
        This refers to how much space a glyph takes up in the line its laid out in. Sometimes this is bigger or smaller than the size of the glyph itself, and is influenced by properties like Kerning and Letter spacing.
        
    Kerning
        When you have a line of text, you put the glyphs next to one another. Sometimes this can lead to little gaps appearing between some glyph combinations. Fonts usually have a list of places where this happens and instruct the text layout to pull the glyphs back a little, so the gap closes. This is called Kerning.
