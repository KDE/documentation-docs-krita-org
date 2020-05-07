.. meta::
   :description:
        Krita's fill tool reference.

.. metadata-placeholder

   :authors: - Wolthera van Hövell tot Westerflier <griffinvalley@gmail.com>
             - Scott Petrovic
   :license: GNU free documentation license 1.3 or later.

.. index:: Tools, Fill, Bucket
.. _fill_tool:

=========
Fill Tool
=========

|toolfill|

Krita has one of the most powerful and capable Fill functions available. The options found in the Tool Options docker and outlined below will give you a great deal of flexibility working with layers and selections.

To get started, clicking anywhere on screen with the fill-tool will allow that area to be filed with the foreground color.

Tool Options
------------

Fast Mode
    This is a special mode for really fast filling. However, many functions don't work with this mode.
Threshold
    Determines when the fill-tool sees another color as a border.
Grow Selection
    This value extends the shape beyond its initial size.
Feathering Radius
    This value will add a soft border to the filled-shape.
Fill Entire Selection
    Activating this will result in the shape filling the whole of the active selection, regardless of threshold.
Use Pattern
    Ticking this will result in the active pattern being used.
Sample
    .. versionadded:: 4.3
    
    Select which layers to use as a reference for the fill tool. The options are:
    
    Current Layer
        Only use the currently selected layer.
    All layers
        Use all visible layers.
    Color Labeled Layers
        Use only the layers specified with a certain color label. This is useful for complex images, where you might have multiple lineart layers. Label them with the appropriate color label and use these labels to mark which layers to use as a reference.

Labels Used
    .. versionadded:: 4.3

    Used with the 'Color Labeled Layers' option above.
