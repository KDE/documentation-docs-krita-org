.. meta::
   :description property=og\:description:
        Understanding font families inside Krita.

.. metadata-placeholder

   :authors: - Wolthera van Hövell tot Westerflier <griffinvalley@gmail.com>
   :license: GNU free documentation license 1.3 or later.

.. index:: Resources, Text, !Fonts
.. _resource_fonts:

=============
Font Families
=============

Since Krita 5.3, Font Families are a resource inside Krita.

Font Families don't correspond to single font files. Instead, they can represent a collection of fonts of varying types. Krita will spend some time trying to organize all the fonts on your system into a proper hierarchy, so you can select fonts as desired while using the text properties like font-weight and font-style to indicate the weight and width you need.

Font families are unique in their localization support. Krita will try to retrieve the correct OpenType names for a given locale, and show those in the UI. It will also try to get an appropriate sample for all the scripts the font supports and display that per-locale.

As resources, font families can be searched and tagged, as well as disabled in the resource manager. Embedding of Font Families is not supported at this moment.

Font Types
----------

The font family picker will show whether the font is an old fashioned bitmap font, a postscript font or an OpenType font (Which can be ether ttf or otf files). Furthermore, it will also show an icon to indicate whether the font is a variable font, or, for color fonts, to indicate which color technologies are available.

Krita doesn't support all color fonts at this time, with only Bitmap and Colrv0 tables supported. Fonts with only SVG and Colrv1 tables will display hex blocks when used.

Adding new fonts
----------------

You can add fonts by installing new fonts on your system, or adding them to the "fonts" folder inside the Krita resource directory. The latter is useful when on a system that doesn't allow installing fonts.

When adding new fonts, Krita will rebuild the internal list of fonts dynamically. However, while new fonts will appear in the fonts list, updating old fonts will require a restart of Krita.
