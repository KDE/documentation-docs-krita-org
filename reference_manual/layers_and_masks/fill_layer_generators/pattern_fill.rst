.. meta::
   :description:
        How to use Pattern fill generation in Krita.

.. metadata-placeholder

   :authors: - Wolthera van Hövell tot Westerflier <griffinvalley@gmail.com>
             - Scott Petrovic
   :license: GNU free documentation license 1.3 or later.

.. index:: Pattern
.. _pattern_fill:

Pattern Fill
------------

This fills the layer with a predefined pattern or texture that has been loaded into Krita through the Resource Management interface. Patterns can be a simple and interesting way to add texture to your drawing or painting, helping to recreate the look of watercolor paper, linen, canvas, hardboard, stone or an infinite other number of options. For example if you want to take a digital painting and finish it off with the appearance of it being on canvas you can add a Fill Layer with the Canvas texture from the texture pack below and set the opacity very low so the "threads" of the pattern are just barley visible.  The effect is quite convincing.

You can create your own and use those as well.  For a great set of well designed and useful patterns check out one of our favorite artists and a great friend of Krita, David Revoy's free texture pack (https://www.davidrevoy.com/article156/texture-pack-1).

Transform
    .. versionadded:: 4.4

    This allows setting a number of transformation options on the pattern, such as scaling or rotating it.
    
    .. figure:: /images/layers/pattern_fill_transform.png
    
       Image showing several transforms applied to a single texture.

    Align to pixel grid
        .. versionadded:: 5.3

        When a geometric transformation is applied to a pattern, the corners of the image that is repeated may be displaced to any new position, including fractional coordinates (sub-pixel, non integer coordinates). This is the default behavior and it is fine most of the times. But there are times when it is desirable that the corners end up at integer coordinates. For example when exact repeatability with pixel accuracy is needed. This can be achieved by checking the *align to pixel grid* option. By doing so, the pattern corners are ensured to fall at integer coordinates after the transformation. Keep in mind that this alignment reduces the number of possible transformations (in fact, all those transformations that map the corners to fractional coordinates are removed), but the aligned transformation will approximate the un-aligned one as close as possible. There is also the possibility of setting every how many repetitions of the pattern the corners should be aligned.

        This option is specially useful when dealing with small patterns, for example those used for screentones, or when the pattern is scaled really small, since it helps reducing some artifacts like moire patterns.

        .. figure:: /images/layers/pattern_fill_align_pixel_grid.png

           *This image shows a pattern fill layer that uses a smiley face image. It is being transformed by scaling to 75% and rotating 34 degrees. On the left no alignment is being applied and on the right the alignment is active and set to every two repetitions, both horizontally and vertically. The blue lines are indicators of the pixel grid and the red ones mark a block of two by two repetitions whose corners are aligned to the pixel grid. Note that, when the alignment is on, then that block is repeated exactly through the image, but when it is off, every instance of the pattern is rendered slightly different.*
