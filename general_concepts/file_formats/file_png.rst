.. meta::
   :description:
        The Portable Network Graphics file format in Krita.

.. metadata-placeholder

   :authors: - Wolthera van Hövell tot Westerflier <griffinvalley@gmail.com>
             - Halla Rempt
   :license: GNU free documentation license 1.3 or later.

.. index:: *.png, PNG, portable network graphics

.. _file_png:

======
\*.png
======

``.png``, or Portable Network Graphics, is a modern alternative to :ref:`file_gif` and with that and :ref:`file_jpg` it makes up the three main formats that are widely supported on the internet.

PNG is a :ref:`lossless <lossless_compression>` file format, which means that it is able to maintain all the colors of your image perfectly. It does so at the cost of the file size being big, and therefore it is recommended to try :ref:`file_jpg` for images with a lot of gradients and different colors. Grayscale images will do better in PNG as well as images with a lot of text and sharp contrasts, like comics.

Like :ref:`file_gif`, PNG can support indexed color and, from the Third Edition, PNG supports animation. Unlike :ref:`file_gif`, this supports full alpha transparency and is not limited to 256 colors. Animated PNG is supported in all major browsers.


.. versionadded:: 4.2
    Since 4.2 we support saving HDR to PNG as according to the `W3C PQ HDR PNG standard <https://www.w3.org/TR/png-hdr-pq/>`_. To save as such files, toggle :guilabel:`Save as HDR image (Rec. 2020 PQ)`, which will convert your image to the Rec 2020 PQ color space and then save it as a special HDR PNG.
