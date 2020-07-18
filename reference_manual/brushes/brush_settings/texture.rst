.. meta::
   :description:
        The texture brush settings option in Krita.

.. metadata-placeholder

   :authors: - Wolthera van Hövell tot Westerflier <griffinvalley@gmail.com>
             - Scott Petrovic
             - Peter Schatz
   :license: GNU free documentation license 1.3 or later.

.. index:: Texture, Patterns
.. _option_texture:

=======
Texture
=======

This allows you to have textured strokes. This parameter always shows up as two parameters:

Texture
-------

Pattern
    Which pattern you'll be using. 
Scale
    The size of the pattern. 1.0 is 100%.

    .. image:: /images/brushes/Krita_2_9_brushengine_texture_05.png
Horizontal Offset & Vertical Offset
    How much a brush is offset, random offset sets a new per stroke.

    .. image:: /images/brushes/Krita_2_9_brushengine_texture_04.png
Texturing mode
    Multiply Alpha
        Uses alpha multiplication to determine the effect of the texture. Has a soft feel.
    Subtract Alpha
        Uses subtraction to determine the effect of the texture. Has a harsher, more texture feel.
        
    .. versionadded:: 4.4
        Lightness and Gradient Map options:
    
    Lightness Map
        Applies lightness values of the texture to the paint.  Can be used to simulate paper/canvas, or for painting a texture, like reptile skin or tree bark.
    Gradient Map
        Maps gray/lightness values of the texture to the currently selected gradient.   Useful for painting textures with multiple colors, like reptile skin, tree bark, stars, etc.
        
    .. image:: /images/brushes/Krita_2_9_brushengine_texture_01.png
    .. image:: /images/brushes/Krita_4_4_brushengine_texture_lightness_gradient_demo.png

Cutoff policy
    Cutoff policy will determine what range and where the strength will affect the textured outcome.

    Disabled
        Doesn't cut off. Full range will be used.
    Pattern
        Cuts the pattern off.
    Brush
        Cuts the brush-tip off.

    .. image:: /images/brushes/Krita_2_9_brushengine_texture_02.png

Cutoff
    Cutoff is... the grayscale range that you can limit the texture to. This also affects the limit takes by the strength. In the below example, we move from the right arrow moved close to the left one, resulting in only the darkest values being drawn. After that, three images with larger range, and underneath that, three ranges with the left arrow moved, result in the darkest values being cut away, leaving only the lightest. The last example is the pattern without cutoff.

    .. image:: /images/brushes/Krita_2_9_brushengine_texture_07.png

Invert Pattern
    Invert the pattern.

    .. image:: /images/brushes/Krita_2_9_brushengine_texture_06.png

Brightness and Contrast

.. versionadded:: 3.3.1

    Adjust the pattern with a simple brightness/contrast filter to make it easier to use. Because Subtract and Multiply work differently, it's recommended to use different values with each:

    .. image:: /images/brushes/Krita_3_1_brushengine_texture_07.png
    
.. versionadded:: 4.4
    Neutral Point adjustment:

Neutral Point
    Adjust the gray value that is considered neutral in the texture.  0.5 keeps the texture as is; higher values make the texture darker, and lower values make the texture lighter.  Works a bit differently from the brightness option, and is mostly useful to adjust existing textures to work well with Lightness Map and Gradient Map modes (though it can have applications with the other two modes).

Strength
--------

This allows you to set the texture to Sensors. It will use the cutoff to continuously draw lighter values of the texture (making the result darker).   

.. versionadded:: 4.4
    For Lightness Map and Gradient Map modes, Strength controls how much of the texture is applied compared to how much of the selected paint color comes through.

.. image:: /images/brushes/Krita_2_9_brushengine_texture_03.png

.. seealso::

    `David Revoy describing the texture feature (old) <https://www.davidrevoy.com/article107/textured-brush-in-floss-digital-painting>`_.
