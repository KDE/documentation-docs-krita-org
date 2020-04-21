.. meta::
   :description:
        How to use fill layers in Krita.

.. metadata-placeholder

   :authors: - Wolthera van Hövell tot Westerflier <griffinvalley@gmail.com>
             - Scott Petrovic
             - Alan
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

Painting on a fill layer
------------------------

A fill-layer is a single-channel layer, meaning it only has transparency. Therefore, you can erase and paint on fill-layers to make them semi-opaque, or for when you want to have a particular color only. Being single channel, fill-layers are also a little bit less memory-consuming than regular 4-channel paint layers.
