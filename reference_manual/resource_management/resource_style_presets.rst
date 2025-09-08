.. meta::
   :description property=og\:description:
        About text style presets inside Krita.

.. metadata-placeholder

   :authors: - Wolthera van Hövell tot Westerflier <griffinvalley@gmail.com>
   :license: GNU free documentation license 1.3 or later.

.. index:: Resources, Text
.. _resource_style_presets:

=============
Style Presets
=============

Style presets allow you to store prefered text properties into a resource. They can be found inside the :ref:`text_properties_docker`, where you can also create new ones or edit preexisting ones:

Name
   The name of the style preset.
Description
   The description will appear as a tool tip while hovering over the style.

Style Presets can be one of two types: paragraph or character, which decides both which properties will be available as well as how the preview is generated.



Style presets are saved as simple SVG text objects with `krita:style-type` added to indicate the type, and `krita:style-resolution` to indicate whether it is a pixel-relative style. SVG Title and Description elements are used to store the name and description.
