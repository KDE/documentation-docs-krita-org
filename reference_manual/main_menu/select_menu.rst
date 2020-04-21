.. meta::
   :description:
        The select menu in Krita.

.. metadata-placeholder

   :authors: - Wolthera van Hövell tot Westerflier <griffinvalley@gmail.com>
             - Scott Petrovic
   :license: GNU free documentation license 1.3 or later.

.. index:: Selection
.. _select_menu:

===========
Select Menu
===========

.. glossary::

    Select All
        Selects the whole layer. Shortcut :kbd:`Ctrl + A`

    Deselect
        Deselects everything (except for active Selection Mask). Shortcut :kbd:`Ctrl + Shift + A`

    Reselect
        Reselects the previously deselected selection. Shortcut :kbd:`Ctrl + Shift + D`

    Invert Selection
        Inverts the selection. Shortcut :kbd:`Ctrl + Shift + I`

    Convert to Vector Selection
        This converts a raster selection to a vector selection. Any layers of transparency there might have been are removed.
        
    Convert to Raster Selection
        This converts a vector selection to a raster selection.
        
    Convert Shapes to Vector Selection
        Convert vector shape to vector selection.

    Convert to Shape
        Converts vector selection to vector shape.

    Display Selection
        Display the selection. If turned off selections will be invisible. Shortcut :kbd:`Ctrl + H`

    Show Global Selection Mask
        Shows the global selection as a selection mask in the layers docker. This is necessary to be able to select it for painting on.

    Scale...
        Scale the selection.

    Select from Color Range...
        Select from a certain color range.

    Select Opaque
        Select all opaque (non-transparent) pixels in the current active layer. If there's already a selection, this will add the new selection to the old one, allowing you to select the opaque pixels of multiple layers into one selection. Semi-transparent (or semi-opaque) pixels will be semi-selected.

    Feather Selection...
        Feathering in design means to soften sharp borders. So this adds a soft border to the existing selection. Shortcut :kbd:`Shift + F6`

    Grow Selection...
        Make the selection a few pixels bigger.

    Shrink Selection...
        Make the selection a few pixels smaller.

    Border Selection...
        Take the current selection and remove the insides so you only have a border selected.

    Smooth
        Make the selection a little smoother. This removes jiggle.
