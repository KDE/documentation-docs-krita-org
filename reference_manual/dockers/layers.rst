.. meta::
   :description property=og\:description:
        Overview of the layers docker.

.. metadata-placeholder

   :authors: - Wolthera van Hövell tot Westerflier <griffinvalley@gmail.com>
             - Scott Petrovic
             - Raghavendra Kamath <raghavendr.raghu@gmail.com>
             - Grum999
   :license: GNU free documentation license 1.3 or later.

.. index:: ! Layers, Passthrough Mode, Alpha Inheritance, Blending Mode, Label, Onion Skin, Layer Style, Alpha Lock, Vector Layer, Anti-aliasing

.. |icon_visible| image:: /images/icons/visible.svg
    :width: 18
.. |icon_novisible| image:: /images/icons/novisible.svg
    :width: 18
.. |icon_locked| image:: /images/icons/locked.svg
    :width: 18
.. |icon_unlocked| image:: /images/icons/unlocked.svg
    :width: 18
.. |icon_alphalocked| image:: /images/icons/bar-transparency-locked.svg
    :width: 18
.. |icon_alphaunlocked| image:: /images/icons/bar-transparency-unlocked.svg
    :width: 18
.. |icon_passthrough-enabled| image:: /images/icons/passthrough-enabled.svg
    :width: 18
.. |icon_passthrough-disabled| image:: /images/icons/passthrough-disabled.svg
    :width: 18
.. |icon_transparency-enabled| image:: /images/icons/transparency-enabled.svg
    :width: 18
.. |icon_transparency-disabled| image:: /images/icons/transparency-disabled.svg
    :width: 18
.. |icon_arrow-up| image:: /images/icons/arrow-up.svg
    :width: 18
.. |icon_arrow-down| image:: /images/icons/arrow-down.svg
    :width: 18
.. |icon_arrow-right| image:: /images/icons/arrow-right.svg
    :width: 18
.. |icon_onion-on| image:: /images/icons/onionOn.svg
    :width: 18
.. |icon_onion-off| image:: /images/icons/onionOff.svg
    :width: 18
.. |icon_layerfx-on| image:: /images/icons/layer-style-enabled.svg
    :width: 18
.. |icon_layerfx-off| image:: /images/icons/layer-style-disabled.svg
    :width: 18
.. |icon_select-shape| image:: /images/icons/select-shape.svg
    :width: 18
.. |icon_select-pixel| image:: /images/icons/select-pixel.svg
    :width: 18
.. |icon_add| image:: /images/icons/list-add.svg
    :width: 18
.. |icon_duplicatelayer| image:: /images/icons/duplicatelayer.svg
    :width: 18
.. |icon_properties| image:: /images/icons/properties.svg
    :width: 18
.. |icon_deletelayer| image:: /images/icons/deletelayer.svg
    :width: 18

.. _layer_docker:

======
Layers
======

.. figure:: /images/dockers/Krita_Layers_Docker.png

    General overview of layer docker for a document with multiple layers


The Layers docker is for one of the core concepts of Krita: :ref:`Layer Management <layers_and_masks>`. You can add, delete, rename, duplicate and do many other things to layers here.


The interface is split in three main parts:

- Controls
- The Layer Stack
- Operations Bar


Controls
--------

At the top there are four controls.

.. image:: /images/dockers/Krita_Layers_Docker_areatop.png
   :alt: Top area of layer docker, with four controls


Blending mode
    .. image:: /images/dockers/Krita_Layers_Docker_blendingmode.png
        :alt: The blending mode dropdown list

    A dropdown list to set the :ref:`Blending mode <blending_modes>` for the active layer.


Opacity
    .. image:: /images/dockers/Krita_Layers_Docker_opacity.png
        :alt: The opacity slider

    A slider to set the opacity for the active layer.


Filter
    .. image:: /images/dockers/Krita_Layers_Docker_filter.png
        :alt: The filter button

    This allows you to filter all existing layers, which can be useful if you have a lot (say, hundreds!) of layers.

    .. figure:: /images/dockers/Krita_Layers_Docker_filterui.png

        Filter option popup from filter button

    Filtering can be applied on:

    - Color labels (available only if there are color label being used, and only used color labels can be filtered)
    - Layer names


Display settings
    .. image:: /images/dockers/Krita_Layers_Docker_displaysettings.png
        :alt: The display settings button

    This allows you to adjust some extra display options of the layer stack.

    .. figure:: /images/dockers/Krita_Layers_Docker_displaysettingsui.png

        Display settings popup from display settings button

    Available display settings are:

    - :guilabel:`Thumbnail size` slider, to let you control the size of layer's thumbnail preview

    - :guilabel:`Tree indentation` slider, lets you control the indentation of sub-layers, for either an expanded or compacted view

    .. _iref-layer_detailmode:

    - The blending mode information, defined by 3 parameters

      .. versionadded:: 5.2

      - Drowpdown :guilabel:`Detail mode`
      
        .. list-table::
           :header-rows: 1
            
           - * Mode
             * Description
           - * :guilabel:`None`
             * No extra information is shown.
           - * :guilabel:`Simple`
             * This will only display the opacity or the blending mode when these are not 100% and :guilabel:`Normal`.
           - * :guilabel:`Balanced`
             * This will display both the opacity and the blending mode for layers where either the opacity is below 100%, or the blending mode is not :guilabel:`Normal`.
           - * :guilabel:`Detailed`
             * This will always show the opacity and blending options for all layers.

      - The :guilabel:`Opacity` slider (enabled if mode is not :guilabel:`None`) allows you to control the opacity of the extra blending info label.
      - The :guilabel:`Inline` checkbox (enabled if mode is not :guilabel:`None`) will provide information on a single compact line.

    .. _iref-layer_checkbox:

    - The :guilabel:`Checkbox for Selecting Layers` enables the extra checkboxes between the visibility icon and the label.

      This is useful for situations where you may not have access to a :kbd:`Ctrl` or :kbd:`Shift` key to select multiple layers, such as on a tablet.





The Layer Stack
---------------

You can select the active layer here. Using the :kbd:`Shift` and :kbd:`Ctrl` keys you can select multiple layers and drag-and-drop them. You can also change the visibility, edit state, alpha inheritance and rename layers. You can open and close groups, and you can drag and drop layers, either to reorder them, or to put them in groups.


.. image:: /images/dockers/Krita_Layers_Docker_arealayerstack.png
   :alt: Layer stack

The Layer Stack is organized in three parts:

- Left side: an eye-icon and :ref:`optional checkbox <iref-layer_checkbox>`
- Middle: layer name and :ref:`optional information <iref-layer_detailmode>`
- Right side: Property controls (available controls will vary according to layer type)


.. glossary::

    Alpha Inheritance
        *Only available on* :ref:`Layers <types_of_layers>`.

        Clicking the alpha inheritance-icon allows you to activate |icon_transparency-enabled| or disable |icon_transparency-disabled|.

        This will use the alpha of all the layers under the active layer, but within the same group, as a transparency mask.

        *Check* :ref:`inherit_alpha_or_clipping_layers` *or* :ref:`clipping_masks_and_alpha_inheritance` *for detailled explanations and examples.*

    Alpha Lock
        *Only available on* :ref:`paint_layers`.

        Clicking the alpha lock-icon will let you lock |icon_alphalocked| or unlock |icon_alphaunlocked| the alpha channel.

        Lock the alpha channel to prevent the transparency of a layer being changed. Useful when coloring images.

    Anti-aliasing
        *Only available on* :ref:`vector_layers`.

        Clicking the anti-aliasing icon to activate |icon_select-shape| or deactivate |icon_select-pixel| the anti aliasing mode.

    Blending Mode
        *Available on all type of* :ref:`Layers <types_of_layers>`.

        This will set the :ref:`blending_modes` of the layer.

    Color Label
        This is a color that you can set on the layer. |mouseright| the layer to get a context menu to assign a color to it. You can then later filter on these colors.
    


    Edit State (Layer lock)
        .. _layer_locked:

        Clicking the lock-icon allow to lock |icon_locked| or unlock |icon_unlocked| the layer.

        Lock the layer prevents any modifications to be made on layer. Useful when handling large amounts of layers or to ensure not modifying a layer's content by mistake.

    Expand or Collapse layers
        *Only available on non-empty* :ref:`group_layers` and :ref:`Layers <types_of_layers>` for which masks are defined.

        Clicking the arrow-icon to expand |icon_arrow-down| or collapse |icon_arrow-right| group/layer.

    Layer Style
        *Only available on* :ref:`Layers <types_of_layers>` *which have a* :ref:`layer_style` *assigned.*

        Clicking the FX-icon allow to quickly activate |icon_layerfx-on| or deactivate |icon_layerfx-off| the layer style.

    Name
        The Layer name, double- |mouseleft| to make it editable, and press the :kbd:`Enter` key to finish editing.

    Onion Skin
        *Only available on* :ref:`animated layers <animation>`

        Clicking the bulb-icon to activate |icon_onion-on| or deactivate |icon_onion-off| onion skin features.

    Opacity
        *Only available on* :ref:`Layers <types_of_layers>`.

        This will set the opacity of the whole layer.

    Pass-through mode
        *Only available on* :ref:`group_layers`.

        Clicking the pass-through mode icon allows you to activate |icon_passthrough-enabled| or deactivate |icon_passthrough-disabled|, which in turns affects how blending modes are composited.

        When active, this allows you to have the blending modes of the layers within affect the layers outside the group.

        Doesn't work with masks currently, therefore these have a strike-through on group layers set to pass-through.

        *Check* :ref:`how_layers_composited_in_krita` *or* :ref:`clipping_masks_and_alpha_inheritance` *for detailled explanations and examples.*


    Visibility
        .. _layer_visibility:

        Clicking the eye-icon allow to show |icon_visible| or hide |icon_novisible| a whole layer.

    Thumbnail Image
        This shows a miniature image with the layer contents. If you :kbd:`Ctrl +` |mouseleft| on it then you can make a selection from the contents of that layer (see `Hot keys and Sticky Keys`_ section below).

    Layer Color Space Mismatch Warning
        .. versionadded:: 5.3
        
        In Krita layers can have a color space different from the color space of the image. It usually happens when you import an external file as a layer. Such difference is a perfectly valid state for Krita, but it may cause visible slowdowns, because Krita will have convert color space of such layers on the fly. When layer's color space is different from the color space a small warning icon is shown next to the layer's properties.

        .. figure:: /images/layers/layer-color-space-mismatch.png
           :align: center
           :figwidth: 800

           "Paint Layer 2" has a color space different from the rest of the image

        To remove the warning you can either manually convert it using :menuselection:`Layer --> Convert --> Convert Layer Color Space` dialog or use :guilabel:`Unify Layers Color Space` action (available via :kbd:`Ctrl + Enter` menu).

To edit these properties on multiple layers at once, press the properties option when you have multiple layers selected or press the :kbd:`F3` key.
There, to change the names of all layers, the checkbox before :guilabel:`Name` should be ticked after which you can type in a name. Krita will automatically add a number behind the layer names. You can change other layer properties like visibility, opacity, lock states, etc. too.

.. versionadded:: 5.0

   By drag-and-dropping colors from the :ref:`palette <palette_docker>` onto the layer stack, you can quickly create a :ref:`fill layer <fill_layers>`.

.. image:: /images/layers/Krita-multi-layer-edit.png


Operations bar
--------------

These are buttons for doing layer operations.

.. image:: /images/dockers/Krita_Layers_Docker_areabtnbar.png
    :alt: Button bar to apply action on layers

Add
    Clicking the |icon_add| button will by default add a new :ref:`Paint Layer <paint_layers>`.

    The little arrow button aside will popup a sub-menu with all available :ref:`layers_and_masks`.

Duplicate
    Clicking the |icon_duplicatelayer| button will duplicate the active layer(s). Can be quickly invoked with the :kbd:`Ctrl +` |mouseleft| :kbd:`+ drag` shortcut.

Move layer up.
    Clicking the |icon_arrow-up| button will move the active layer up. Will switch them out and in groups when coming across them.

Move layer down.
    Clicking the |icon_arrow-down| button will move the active layer down. Will switch them out and in groups when coming across them.

Layer properties.
    Clicking the |icon_properties| button open the layer properties window.

    The little arrow button aside will popup the |mouseright| context menu for the currently selected layer. This is useful when you don't have access to a |mouseright| button.

Delete
    Clicking the |icon_deletelayer| button will delete the active layer(s). For safety reasons, you can only delete :ref:`visible <layer_visibility>` and :ref:`unlocked <layer_locked>` layers.


Hot keys and Sticky Keys
------------------------

* :kbd:`Shift` key for selecting multiple contiguous layers.
* :kbd:`Ctrl` key for select or deselect layer without affecting other layers selection.
* :kbd:`Ctrl +` |mouseleft| :kbd:`+ drag` shortcut makes a duplicate of the selected layers, for you to drag and drop.
* :kbd:`Ctrl + E` shortcut for merging a layer down. This also merges selected layers, layer styles and will keep selection masks intact. Using the :kbd:`Ctrl + E` shortcut on a single layer with a mask will merge down the mask into the layer.
* :kbd:`Ctrl + Shift + E` shortcut merges all layers.
* :kbd:`R +` |mouseleft| shortcut allows you to select the top layer with content below the cursor as the active layer. In addition to this, you can set shortcuts for 4 other modes:
    - "Select All Layers (Replace Selection)" allows you to select all layers with content below the cursor as the currently selected layers.
    - "Select All Layers (Add to Selection)" allows you to select all layers that have content below the cursor and add them to the selected layers.
    - "Select from Menu (Replace Selection)" allows you to select a layer from a pop-up menu or all layers in the menu as the active layer or active layers.
    - "Select from Menu (Add to Selection)" allows you to select all layers in the menu as the new active layer or active layers. The latter two modes are similar to using :kbd:`Ctrl +` |mouseright| to select a layer in Photoshop.
* :kbd:`Ins` key for adding a new layer. 
* :kbd:`Shift + Ins` key for adding a new vector layer.
* :kbd:`Ctrl + G` shortcut will create a group layer. If multiple layers are selected, they are put into the group layer.
* :kbd:`Ctrl + Shift + G` shortcut will quickly set-up a clipping group, with the selected layers added into the group, and a new layer added on top with alpha-inheritance turned on, ready for painting!
* :kbd:`Ctrl + Alt + G` shortcut will ungroup layers inside a group.
* :kbd:`Alt +` |mouseleft| shortcut for isolated view of a layer. This will maintain between layers till the same action is repeated again.
* :kbd:`Page Up` and :kbd:`Page Down` keys for switching between layers.
* :kbd:`Ctrl + Page Up` and :kbd:`Ctrl + Page Down` shortcuts will move the selected layers up and down.
* :kbd:`Ctrl +` |mouseleft| over a layer's thumbnail to replace the current selection with a new one created from the contents of that layer.
* :kbd:`Ctrl + Shift +` |mouseleft| over a layer's thumbnail to add a new selection created from the contents of that layer to the current selection.
* :kbd:`Ctrl + Alt +` |mouseleft| over a layer's thumbnail to subtract a new selection created from the contents of that layer from the current selection.
* :kbd:`Ctrl + Shift + Alt +` |mouseleft| over a layer's thumbnail to intersect the current selection with a new selection created from the contents of that layer.


