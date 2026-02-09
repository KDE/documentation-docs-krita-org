.. meta::
   :description lang=en:
        Krita's Comic Panel Editing Tool reference.

.. metadata-placeholder

   :authors: - Agata Cacko <cacko.azh@gmail.com>
   :license: GNU free documentation license 1.3 or later.

.. index:: Tools, Vector, Comic, Panel
.. _comic_panel_editing_tool:

========================
Comic Panel Editing Tool
========================

|toolcomicpanelediting|

The Comic Panel Editing Tool allows you to slice through vector shapes, adding a gap or gutter in between the resulting halves. Then it also allows you to remove the gaps.

Tool Options
------------

**Cutting mode**

|toolcomicpanelediting_cutting|

This mode allows you to cut through shapes and create gaps (gutters) of a specified width.

Note: you need to first create a vector layer, and on a vector layer create the initial shape. For example, for a classic comic, use the :ref:`rectangle_tool` on a vector layer for the rectangle encompassing all panels.

To create a gap between shapes, press and drag, until the line crosses all the shapes you want to cut through.


Unit of width
    Defines the unit of width used for the presets below.
Thick Gap, Thin Gap, Special Gap
    Three presets for your three most used gap widths.
Automatic
   This option allows Krita to select the most appropriate gap width preset based on the angle of the line.
Horizontal
   In :guilabel:`Automatic` mode, if the line is horizontal based on the :guilabel:`Angle`, choose the specified gap width preset for the gap.
Vertical
   In :guilabel:`Automatic` mode, if the line is vertical based on the :guilabel:`Angle`, choose the specified gap width preset for the gap.
Diagonal
   In :guilabel:`Automatic` mode, if the line is diagonal based on the :guilabel:`Angle`, choose the specified gap width preset for the gap.
Angle
   In :guilabel:`Automatic` mode, if the angle between the line and a perfectly horizontal line is smaller than the :guilabel:`Angle`, use the preset specified by :guilabel:`Horizontal`; 
   if the angle between the line and a perfectly vertical line is smaller than the :guilabel:`Angle`, use the preset specified by :guilabel:`Vertical`; otherwise, use the preset specified by :guilabel:`Diagonal`.

**Merging mode**

|toolcomicpanelediting_merging|

Remove the gutter between shapes.

To remove the gap, press on one side of the gap, drag and release on the other side of the gap. Note that you can only remove one gap at a time, and the gap removing line must cross exactly two shape edges for it to work correctly.