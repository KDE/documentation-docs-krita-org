.. meta::
   :description:
        How to use vector layers in Krita.

.. metadata-placeholder

   :authors: - Wolthera van Hövell tot Westerflier <griffinvalley@gmail.com>
             - Scott Petrovic
             - ValerieVK
             - Lifeling
             - JohnS
             - Leovilok
             - Grum999
   :license: GNU free documentation license 1.3 or later.

.. index:: Vector, Layers

.. |icon_vectorlayer| image:: /images/icons/vectorLayer.svg
    :width: 18
.. |icon_add| image:: /images/icons/list-add.svg
    :width: 18
.. |icon_arrange_back| image:: /images/icons/action-object-order-back-calligra.svg
    :width: 18
.. |icon_arrange_front| image:: /images/icons/action-object-order-front-calligra.svg
    :width: 18
.. |icon_arrange_raise| image:: /images/icons/action-object-order-raise-calligra.svg
    :width: 18
.. |icon_arrange_lower| image:: /images/icons/action-object-order-lower-calligra.svg
    :width: 18
.. |selectshape| image:: /images/icons/select-shape.svg
    :width: 18
.. |selectpixel| image:: /images/icons/select-pixel.svg
    :width: 18

.. _vector_layers:

=============
Vector Layers
=============


What is a Vector Layer?
-----------------------

A Vector Layer, also known as a Shape Layer, is a type of layers that contains only vector graphics elements.

The vector layer appear in :program:`Krita`'s :ref:`Layers docker <layer_docker>` with the following icon |icon_vectorlayer| right to the layer thumbnail.

.. image:: /images/vector/Vectorlayer.png


.. admonition:: About Vector Graphics & Raster Images

    :program:`Krita` is primarily a `Raster Graphics <https://en.wikipedia.org/wiki/Raster_graphics>`__ editing tool, which means that most of the editing changes the values of the pixels on the raster that makes up the image.

    A `Vector Graphics <https://en.wikipedia.org/wiki/Vector_graphics>`__ editing tool will use mathematics to describe shapes. Shapes can be edited at any time (modified, deleted). Because it uses formulas, vector graphics can be resized to any size without any 'pixel' or 'blur' effect.

    Vector Graphics are useful to generate logo and banners. They're also useful to manipulate and render texts (a vector graphic text can be edited where a rasterized text can't).



Creating a Vector Layer
-----------------------

In :ref:`Layers docker <layer_docker>`, click on dropdown arrow right to the *Add layer* |icon_add| button; this will popup a sub-menu with the :guilabel:`Add Vector Layer` entry.

Default shortcut to create a new vector layer is :kbd:`Shift + Ins`.


Creating Shapes
---------------

When active layer is a vector layer, the following tools can be used to create vector shapes.

Specialized vector shapes
    Krita provides differents specialized vector shapes tools:

    - |toolcalligraphy| :ref:`calligraphy_tool`
    - |toolellipse| :ref:`ellipse_tool` (also allow to create pie shapes)
    - |toolrectangle| :ref:`rectangle_tool` (also allow to create rounded rectangle shapes)

Paths shapes
    Krita provides differents paths shapes tools:

    - |toolbeziercurve| :ref:`bezier_curve_tool`
    - |toolfreehandpath| :ref:`freehand_path_tool`
    - |toolline| :ref:`line_tool`
    - |toolpolygon| :ref:`polygon_tool`
    - |toolpolyline| :ref:`polyline_tool`


Text shapes
    - |tooltext| :ref:`text_tool`


Import of SVG document
    In addition, you can import a `Scalable Vector Graphic <https://en.wikipedia.org/wiki/SVG>`__ (SVG):

    - Paste a SVG content copied from another software like `Inkscape <https://inkscape.org/>`__ for example
    - Open a SVG file in a new document, edit Vector Layer content, copy/paste it or copy/paste shapes from it


Arranging Shapes
----------------

A vector layer has its own hierarchy of shapes, also named *z-Order*.

When a Vector Layer is rendered, shapes are drawn from the bottom to the top:

+-------------------------------------------+------------------------------------------+
| .. figure:: /images/vector/arrange00.png  | .. figure:: /images/vector/arrange01.png |
|                                           |                                          |
|    *z-Order* Visualization of shapes      |    Rendered image from shapes            |
|                                           |                                          |
+-------------------------------------------+------------------------------------------+

The *z-Order* of shapes can be modified in 2 way:

- From :ref:`Docker Arrange <arrange_docker>`
- From context menu, accessible with |mouseright|

Both provides the same functions:

- |icon_arrange_front| Bring to Front: move *z-Order* position to the top
- |icon_arrange_raise| Raise: move *z-Order* position on step up
- |icon_arrange_lower| Lower: move *z-Order* position on step down
- |icon_arrange_back| Send to Back: move *z-Order* position to the bottom

+------------------------------------------+
| .. figure:: /images/vector/arrange02.png |
|                                          |
|    Red square has been "Bring to front"  |
+------------------------------------------+


Selecting Shapes
----------------

To manipulate shapes, you need to select them with the :ref:`shape_selection_tool` |toolshapeselection|.

The :ref:`shape_selection_tool` also provides access to options to manage shape geometry, stroke and fill properties.



Editing Shapes Outline
----------------------

Outline for a shape can be edited with the :ref:`shape_edit_tool` |toolshapeedit|.



Rendering Vector Layer content
------------------------------

By default, vector layer content are rendered using an anti-aliasing algorithm.

.. image:: /images/vector/antialiasing.png
    :width: 800

- | In the :ref:`Layers docker <layer_docker>` the vector layer icon |selectpixel| indicates the anti-aliasing is disabled
  | On blue vector shapes, you can see aliased pixels in magnified view

- | In the :ref:`Layers docker <layer_docker>` the vector layer icon |selectshape| indicate the anti-aliasing is enabled
  | On pink vector shapes, you can see anti-aliased pixels in magnified view






