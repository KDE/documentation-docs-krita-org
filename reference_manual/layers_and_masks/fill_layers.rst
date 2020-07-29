.. meta::
   :description:
        How to use fill layers in Krita.

.. metadata-placeholder

   :authors: - Wolthera van Hövell tot Westerflier <griffinvalley@gmail.com>
             - Scott Petrovic
             - Alan
             - L. E. Segovia <amy@amyspark.me>
   :license: GNU free documentation license 1.3 or later.

.. index:: Layers, Fill, Generator
.. _fill_layers:

===========
Fill Layers
===========

A Fill Layer is a special layer that Krita generates on-the-fly that can contain either a pattern or a solid color.

.. image:: /images/layers/Fill_Layer.png

Color
    Fills the layer with a singular color. Since version 4.2, newly created colored fill layers will be assigned to the currently active foreground color.

Pattern
    This fills the layer with a predefined pattern or texture that has been loaded into Krita through the Resource Management interface. Patterns can be a simple and interesting way to add texture to your drawing or painting, helping to recreate the look of watercolor paper, linen, canvas, hardboard, stone or an infinite other number of options. For example if you want to take a digital painting and finish it off with the appearance of it being on canvas you can add a Fill Layer with the Canvas texture from the texture pack below and set the opacity very low so the "threads" of the pattern are just barley visible.  The effect is quite convincing.

    You can create your own and use those as well.  For a great set of well designed and useful patterns check out one of our favorite artists and a great friend of Krita, David Revoy's free texture pack (https://www.davidrevoy.com/article156/texture-pack-1).

    Transform
        .. versionadded:: 4.3.1

        This allows setting a number of transformation options on the pattern, such as scaling or rotating it.

SeExpr
    .. versionadded:: 4.3.1

    .. image:: /images/layers/SeExpr-David-Revoy.jpg

    Fills the layer with a pattern specified through Disney Animation's
    `SeExpr expression language <https://wdas.github.io/SeExpr>`_.

    .. seealso::
        - :ref:`seexpr_tut_intro`
        - :ref:`seexpr`
        - `Inigo Quilez's articles <https://iquilezles.org/www/index.htm>`_
        - `The Book of Shaders <https://thebookofshaders.com/>`_

    SeExpr is an embeddable, arithmetic expression language that enables you to
    write shader-like scripts. Through this language, Krita can add dynamically 
    generated textures like lava (example above), force fields, wood, marble, 
    etc. to your layers.

    As with Patterns, you can create your own and use those as well.
    For some examples, please check out the thread `"Procedural texture generator (example and wishes)" on Krita Artists <https://krita-artists.org/t/procedural-texture-generator-example-and-wishes/7638>`_.
    You can download them as a bundle through `Amyspark's blog <https://www.amyspark.me/blog/posts/2020/07/03/third-alpha-release.html>`_.

    Script
        Select the desired preset out of any existing bundled presets.
        This tab is identical to the Pattern preset selector.

        .. image:: /images/seexpr/SeExpr_script.png

    Options
        This tab allows you to edit the selected preset, and apply its script 
        to the layer.

        .. image:: /images/seexpr/SeExpr_editor.png

        There are three sections. The first bar allows you to edit and save the selected preset:

        .. image:: /images/seexpr/SeExpr_editor_preset_mgmt.png

        If your script is syntactically correct, the middle box lets you
        adjust its variables through widgets.

        .. image:: /images/seexpr/SeExpr_editor_widgets.png

        The lower box contains the script text, and shows the detected syntax 
        errors, if any.

        .. image:: /images/seexpr/SeExpr_editor_script_error.png

        You can adjust how much space the latter two boxes have through their
        splitter.

Simplex Noise
    .. versionadded:: 4.2

    .. image:: /images/layers/fill_layer_simplex_noise.png

    This fills the layer with generated OpenSimplex noise. OpenSimplex is different from the more common Perlin noise (often named 'clouds' in other software) and also different from Improved Perlin noise. OpenSimplex has less dimensional artifacts (the subtle "checker" texture often found high frequency Perlin noise) and is a ubiquitous open standard. Since OpenSimplex noise is important to texture generation, this fill layer has the option
    to loop around the canvas edge. You can read more about OpenSimplex `here
    <https://en.wikipedia.org/wiki/OpenSimplex_noise>`_.

    There are a few different use cases for simplex noise. One of these is to create interesting looping patterns, achieved by stacking multiple simplex noise fills with different blending modes. It becomes even more expressive when combined with the levels adjustment layers. For texture artists, this can be a useful utility when combined with a gradient map filter layer to provide color diversity to a looping texture.
    For traditional artists, simplex noise layers can be converted to selection masks to create brush transparency dynamics and masking effects. Experimenting with different combinations can be fun and produce interesting results!

    Looping
        Whether or not to force the pattern to loop.
    Frequency
        The frequency of the waves used to generate the pattern. Higher frequency results in a finer noise pattern.
    Ratio
        The ratio of the waves in the x and y dimensions. This makes the noise have a rectangular appearance.
    Use Custom Seed
        The seed for the random component. You can input any value or text here, and it will always try to use this value to generate the random values with (which then are always the same for a given seed). Leaving the value empty will use the randomly-assigned seed value on layer creation.

Screentone
    .. versionadded:: 4.3.1

    Fills the layer with simple regular patterns like dots and lines like the ones used in traditional `screentone <https://en.wikipedia.org/wiki/Screentone>`_ or `halftone <https://en.wikipedia.org/wiki/Halftone>`_ techniques.

    Screentone Type
        Pattern
            Select the global appearance (dots, lines).
        Shape
            Select the specific appearance of the pattern (for example: round dots, diamond dots, straight lines, sine wave lines).
        Interpolation
            Select how the pattern transitions from the foreground to the background.

            In most cases but the dot pattern with round shape combination, the effect of the interpolation mode is not very noticeable.

        .. figure:: /images/layers/fill_layer_screentone_type.png

            From left to right, top to bottom: 
            dot pattern with round shape, dot pattern with ellipse shape, 
            dot pattern with diamond shape, dot pattern with square shape, 
            line pattern with straight shape, line pattern with sine wave shape, line pattern with triangular wave shape, 
            line pattern with sawtooth wave shape and line pattern with curtain shape.

    Transformation
        Select how the pattern is arranged geometrically in the image (position, size, rotation, shear).  
        Some patterns benefit from the capability of choosing horizontal and vertical sizes separatelly. For example, the sin wave lines pattern has a small period by default and by choosing a large horizontal size the period will look also larger.
    
        .. figure:: /images/layers/fill_layer_screentone_transformation.png

            From left to right: 
            dot pattern with round shape without rotation, dot pattern with round shape and rotated 45 degrees, 
            line pattern with sine wave shape and a size of 20px horizontally and vertically, 
            line pattern with sine wave shape and a size of 50px horizontally and 20px vertically.

    Postprocessing
        Background & Foreground
            Allows you to choose the color and opacity of the foreground (dots, lines) and the background.
        Invert
            This flips what is treated as foreground and background.
        Brightness & Contrast
            The brightness controls how close to the foreground or background color the pattern apperars (how *dark* or *light* in the case of black foreground and white background). 
            So if you want to simulate small dots, for example, set the brightness to a high value and to obtain big dots set it to a low value.
            
            The contrast controls how smooth or sharp is the transition between the foreground and background colors. By default the contrast is set to 50% (smooth). 
            To achieve the typical sharp borders the contrast must be set to a higher value.

        .. figure:: /images/layers/fill_layer_screentone_postprocessing.png

            First row: different combinations of foreground and background colors. 
            Second row, from left to right: 25%, 50% and 75% brightness with 90% contrast. 
            Third row, from left to right: 25%, 50% and 75% contrast with 50% brightness. 

Painting on a fill layer
------------------------

A fill-layer is a single-channel layer, meaning it only has transparency. Therefore, you can erase and paint on fill-layers to make them semi-opaque, or for when you want to have a particular color only. Being single channel, fill-layers are also a little bit less memory-consuming than regular 4-channel paint layers.
