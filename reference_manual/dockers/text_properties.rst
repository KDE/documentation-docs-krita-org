.. meta::
   :description property=og\:description:
        Overview of the text properties docker.

.. metadata-placeholder

   :authors: - Wolthera van Hövell tot Westerflier <griffinvalley@gmail.com>
   :license: GNU free documentation license 1.3 or later.

.. index:: Text
.. _text_properties_docker:

======================
Text Properties Docker
======================

The text properties docker allows you to edit text properties of text objects currently selected with either the :ref:`shape_selection_tool` or :ref:`text_tool`.

By default, the docker will show only a handful of basic properties, while all other properties are only shown when they are relevant, with relevant meaning they are currently set, or :term:`inherited`.

The revert button before a given property will give an indicator of whether a property is set, and clicking it will unset the property, reverting it to either the default or inherited value. When a mixture of style properties are selected, you will see a multi-headed arrow, while the control itself will show the default or inherited value. Modifying the control will set the same value on all properties, while clicking the revert button will unset the property on all text.

New properties can be added with the "add property" dropdown below. The text input allows for searching the current text properties, with each property having a number of alternate keywords.

The visibility state of each property can be configured by pressing the "configure button" next to the "add properties" dropdown. When the default visibility is set to "always show" and none of the individual properties are set to show conditionally, the "add property" dropdown is replaced with a filter input. The current visibility states are possible:

Follow Default
    The property will follow the default visibility state at the top of the configuration window.
Always Visible
    The property will always be visible.
When Set
    The property will be visible only when set.
When Relevant
    The property will be visible when it is set or when it is inherited.
Never Show
    The property is never shown.

Inheritance
-----------

Krita's text shape uses CSS, and thus allows for properties to be inherited. This means that properties like the font size can be set over a whole text shape, and ranges of text within the shape will default to the inherited value if it is not explicitly set on the range.

Some properties allow for font relative units. The meaning of these units also depend on inheritance mechanics. All font relative units will try to use the current font metrics. However, when said font metric is :ref:`_text_property_font_size` or :ref:`_text_property_line_height` related, and the property being edited is one of those itself, it will instead be relative to the inherited size.

Em
    The current font size (or inherited font size in the case of Font Size).
Ex
    The current x height. This metric is retrieved from the font, and affected by font size.
Cap
    The current capital height. This metric is retrieved from the font, and affected by font size.
Lh
    The line-height. This is either relative to the current line height or, in the case of :ref:`_text_property_line_height`, the inherited line height.
Ic
    Relative to ideographic character advance. The advance of a single CJK character. 
Char
    Advance of the number '0'.

Conversely, some properties do not inherit at all. These properties usually get added on top of one another, but the precise behaviour is described in their entry:

Character Properties
--------------------

Character properties are properties that can be applied on a range of text or the whole paragraph.

.. _text_property_font_size:

Font Size
~~~~~~~~~

Font size allows setting the size of the characters.

By default, this property is always visible.

.. _text_property_font_size_adjust:

Font Size Adjust
~~~~~~~~~~~~~~~~

Font size adjust allows setting a ratio that the x-height must be matched by.

.. _text_property_font_family:

Font Family
~~~~~~~~~~~

Font family allows selecting a list of fonts that should be used for the current text. The first font family is the primary font used, while each font family after that is used for fallback.

See :ref:`resource_fonts` for more information about the font picker and font families.

By default, this property is always visible.

.. _text_property_font_style:

Font Style
~~~~~~~~~~

Font style allows setting the sub style of the given font family, such as italics and bold.

The main control is a drop down that shows a list of predefined styles. These are determined either by the fonts within a family, or by the instances inside a variable font. Clicking any of these will set the corresponding CSS properties for that style.

When unfolding this property, the following settings are available:

Weight
    This controls the thickness of the glyph outlines.
Synthesize Weight
    This allows synthesizing thick glyphs when there's no support for bold in the font family.
Width
    This controls how much horizontal space a glyph takes. Not all fonts support this, and there's no synthesis for this.
Slant
    This can be either :guilabel:`Normal`, :guilabel:`Italic` or :guilabel:`Oblique`. The difference between Italic and Oblique is that the former corresponds to a glyph style remniscent of the Italic calligraphy style, while the latter is a slanted version of the normal glyphs.
    
    When :guilabel:`Oblique` is selected, the angle can also be configured. This is primarily for use with variable fonts that support the slant axis.
Synthesize Slant
    This allows synthesizing slanted glyphs where there's no italic or oblique version of the glyphs available.
Optical Size
    This determines whether the optical size axis in Variable Fonts will be synced to the font size. Note that Krita interprets the axis value to be in points.

Finally, there's a place for the extra axes. These are for use with variable fonts, which can provide more configuration for the font style.

This property is by default, always visible.

.. _text_property_letter_spacing:

Letter Spacing
~~~~~~~~~~~~~~

Letter spacing controls the spacing between visible clusters of characters.

.. _text_property_word_spacing:

Word Spacing
~~~~~~~~~~~~

Word spacing controls the size of word-break characters, such as the space character.

.. _text_property_line_height:

Line Height
~~~~~~~~~~~

Line Height controls the line height used for the range of text.

.. _text_property_line_break:

Line Break
~~~~~~~~~~

Line Break allows choosing a strictness for the line breaking algorithm. Mostly used for CJK scripts, requires language being set.

.. _text_property_word_break:

Word Break
~~~~~~~~~~

Word Break allows fine-tuning the line breaking by toggling whether to only break at words or also allow breaking at characters. Useful for Korean or Ethiopian.

.. _text_property_text_transform:

Text Transform
~~~~~~~~~~~~~~

Text Transform allows transforming the given range of characters, for example, by setting them uppercase, or switching out half-width forms for full-width forms.

Text Decoration does not inherit. Instead it is applied over each range of text it is defined on, with later defined text decoration being drawn on top of earlier defined text decoration.

.. _text_property_text_decoration:

Text Decoration
~~~~~~~~~~~~~~~

Text Decoration allows drawing underlines, overlines and striking through text.

.. _text_property_underline_position:

Underline Position
~~~~~~~~~~~~~~~~~~

Specify the position of the underline for text-decoration.

.. _text_property_open_type:

OpenType Features
~~~~~~~~~~~~~~~~~

OpenType Feature Settings

This provides precise control over Open Type features. OpenType features are usually defined by tags, and whether they are on or off. The dropdown will provide a list of features in the primary font in the :ref:`text_property_font_family` list.

For where it is feasible, a small preview is rendered, but for some features it can be hard to provide this.

Typing in a feature name or tag into the search will show a filtered list of all official features that match the search. This way, features that are not shown in the drop down can still be selected and enabled.

See also the :ref:`glyph_palette` for an alternate way of selecting glyph alternates in the current text.

OpenType features, while they inherit, inherit as one list. If you want to give general hints for a given feature to be enabled over the whole text, use the Glyph properties:

Glyphs: Ligatures
    Enable or disable ligatures and contextual alternates on the text.
Glyphs: Position
    Enable super or subscripts on the text.
Glyphs: Numeric
    Enable number-related glyph forms on the text.
Glyphs: Caps
    Enable opentype features related to capitals, such as small caps.
Glyphs: East-Asian
    Enable glyph forms related to East Asian text layout.
Font Kerning
    Turn font kerning on or off. Font kerning enables per-glyph spacing adjustments.

.. _text_property_direction:

Direction
~~~~~~~~~

Direction sets whether the text is left-to-right or right-to-left.

Unicode Bidi:

Unicode bidi is one of the properties that does not inherit. The reason for this is that it works by inserting bi directional algorithm controls at the ends of the given range. When setting the unicode bidi controls inside another set of unicode bidi controls, multiple sets of controls will be added inside each other.

.. _text_property_baseline:

Baseline
~~~~~~~~

In some script traditions, the alignment point of text of different sizes are different from the alignment point with Latin text. For compatibility purposes, fonts of these scripts are usually made so the glyphs align properly with Latin text. To achieve a more traditional alignment, dominant and alignment baseline can be used.

This feature will try to use data encoded in the fonts' baseline table. If there's no such data, the baseline metrics will be auto-generated.

Dominant Baseline
    Dominant Baseline specifies how stretches of text of different sizes are aligned, it is also the default for Alignment Baseline.

Alignment Baseline
    Alignment Baseline allows control over how this range of text is aligned to the parent text.
    
    Alignment baseline does not inherit. Instead, child text will try to align to the specified baseline of the parent text.

Baseline Shift
    Baseline shift allows moving the text away from the baseline, either by predefined super and subscript values, or by a fixed amount.
    
    Baseline shift does not inherit. What instead happens is that shifts will be added to one another, allowing the following:

.. _text_property_white_space:

White Space
~~~~~~~~~~~~

The CSS white space rule controls how multiples of spaces are handled, and whether the text can wrap.

By default, this property is hidden.

.. _text_property_language:

Language
~~~~~~~~

The language of this text shape. Language affects a number of properties, like glyph shape, upper- and lowercase and line breaking.


Paragraph Properties
--------------------

Paragraph properties are the properties that can only be applied over a whole text shape.

.. _text_property_writing_mode:

Writing Mode
~~~~~~~~~~~~

Writing Mode sets whether the text flows horizontally or vertically, and in the latter case, whether the block flows right to left or left to right.

See also :ref:`text_property_direction`.

A related feature is "Text Orientation", which allows rotating horizontal text when it is typeset vertically. Krita does not current support this feature, but it is planned in the future.

.. _text_property_text_indent:

Text Indent
~~~~~~~~~~~

Text Indent allows setting indentation at the line start. Only works when the text is wrapping.

.. _text_property_text_align:

Text Align
~~~~~~~~~~

Text Align sets the alignment for the given block of characters.

The main control of this shows three buttons that correspond to start, middle and end. These properties are affected by direction, meaning that right to left text, start will be the same as align right. The final button is the justification toggle.

By default, this property is always visible, even when not set.

.. _text_property_hanging_punctuation:

Hanging Punctuation
~~~~~~~~~~~~~~~~~~~

Hanging punctuation allows hanging opening and closing punctuation as well as commas. This implementation only implements East-Asian style hanging punctuation.

.. _text_property_tab_size:

Tab Size
~~~~~~~~

Tab Size allows defining the size of tabulation characters. Tabulation characters (inserted with :key:`tab`) are a type of white space that snaps to the nearest multiple of the reference size. Its main use case is to align columns of information without resorting to tables.

.. _text_property_text_rendering:

Text Rendering
~~~~~~~~~~~~~~

Text Rendering controls the hinting and rendering style for the text shape.

Optimize Speed
    The hinting style used for monochrome bitmaps is used, and anti-aliasing is turned off. Krita will also take care to snap the glyphs to the nearest pixel. This allows for pixel art fonts to look good, as well as being the most performant option.
Optimize Legibility
    In vertical writing modes, full hinting is enabled, while for horizontal, hinting only happens vertically. Krita will additionally snap relevant metrics in these directions.
Geometric Precision
    No hinting is performed at all.
Auto
    Same as :term:`Geometric Precision`.

.. _text_docker_style_presets:

Style Presets
-------------

:ref:`resource_style_presets` allow storing combinations of properties for later use. See that page for information about editing style presets.

Clicking an entry will select it for editing, while double clicking will apply the active properties onto the text.

The buttons at the bottom allow modifying the style presets:

Import Style Presets
    Import an SVG with a style preset definition inside.
Delete Style Presets
    Disable a given style preset.
Create Style Preset
    Creates a style preset from the current settings.
Clone Preset
    Clones the current presets and shows the edit window.
Edit Preset
    Edits the current selected presets.

