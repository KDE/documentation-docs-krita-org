.. meta::
    :description:
        Deswcription of the Krita File Format

.. metadata-placeholder

    :authors: - Boudewijn Rempt <boud@valdyas.org>
              - Wolthera van Hövell tot Westerflier <griffinvalley@gmail.com>
    :license: GNU free documentation license 1.3 or later.
    
.. _kra_the_krita_file_format.rst:

==========================
KRA: The Krita File Format
==========================

Krita files have the file name extension .kra. The data is stored within a ZIP file wrapper. Krita can save both as 32 bit as well as 64 bit zip files, depending on the user's settings. Applications reading .kra files should not make any assumptions about compression settings, but only DEFLATED and STORED are used to add files to the store.

The format is similar to the OpenRaster and OpenDocument documents.

This file format is hereafter referred to as a “kra file” in this specification. It has a number of required and optional standard files and subdirectories within it:

::

    example.kra  [considered as a folder-like object]
     ├ mimetype
     ├ documentinfo.xml
     ├ maindoc.xml
     ├ example/
     │  ├ layers/
     │  │   ├ layer
     │  │   ├ layer1.defaultpixel
     │  │   ├ layer1.icc
     │  │   └ layer2.shapelayer/content.svg
     │  ├ palettes/  
     │  │   └ palette.kpl
     │  ├ annotations/
     │  │   ├ proofing/icc
     │  │   └ icc
     │  └ reference_images/
     │      ├ 0.png
     │      └ 1.png
     ├ preview.png
     └ mergedimage.png
     
Required Files
--------------

mimetype
~~~~~~~~

The first file in the archive must be called ``"mimetype"``, without a
file name extension. It must be STORED without compression. This file
must contain the string ``"application/x-krita"``, with no whitespace or
trailing newline.

documentinfo.xml
~~~~~~~~~~~~~~~~

This is an UTF-8 encoded XML file that contains information about the document.
It follows an old-pre OpenDocument specification of which the DTD is no longer
available

::

    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE document-info PUBLIC '-//KDE//DTD document-info 1.1//EN' 'http://www.calligra.org/DTD/document-info-1.1.dtd'>
    <document-info xmlns="http://www.calligra.org/DTD/document-info">
        <about>
            <title>example</title>
            <description></description>
            <subject></subject>
            <abstract><![CDATA[]]></abstract>
            <keyword></keyword>
            <initial-creator>Unknown</initial-creator>
            <editing-cycles>1</editing-cycles>
            <editing-time></editing-time>
            <date>2020-02-20T15:13:34</date>
            <creation-date>2020-02-20T15:13:25</creation-date>
            <language></language>
            <license></license>
    </about>
    <author>
        <full-name></full-name>
        <creator-first-name></creator-first-name>
        <creator-last-name></creator-last-name>
        <initial></initial>
        <author-title></author-title>
        <position></position>
        <company></company>
    </author>
    </document-info>


maindoc.xml
~~~~~~~~~~~

This is an UTF-8 encoded XML file that describes the document structure. There is *no* formal definition for ``maindoc.xml`` and the DTD has long since been lost, after it had become unmaintained. In other words, it's defined by example and new versions of Krita will define new sections. Even if the document does not contain an animation, and animation section is present.

::

    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE DOC PUBLIC '-//KDE//DTD krita 2.0//EN' 'http://www.calligra.org/DTD/krita-2.0.dtd'>
    <DOC xmlns="http://www.calligra.org/DTD/krita" syntaxVersion="2" editor="Krita" kritaVersion="4.3.0-prealpha">
        <IMAGE description="" name="example" mime="application/x-kra" profile="sRGB-elle-V2-srgbtrc.icc" x-res="100" width="1600" y-res="100" colorspacename="RGBA" height="1200">
            <layers>
                <layer colorlabel="0" x="0" onionskin="0" filename="layer" locked="0" collapsed="0" opacity="255" compositeop="normal" nodetype="paintlayer" name="Layer 1" colorspacename="RGBA" visible="1" y="0" selected="true" uuid="{e19a06e3-7990-4ece-a152-a57df805643f}" intimeline="1" channelflags="" channellockflags=""/>
            </layers>
            <ProjectionBackgroundColor ColorData="AAAAAA=="/>
            <GlobalAssistantsColor SimpleColorData="176,176,176,255"/>
            <palettes>
                <palette filename="New_Palette.kpl"/>
            </palettes>
            <animation>
                <framerate value="24" type="value"/>
                <range from="0" to="100" type="timerange"/>
                <currentTime value="0" type="value"/>
            </animation>
        </IMAGE>
    </DOC>

example (image data directory)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This directory has the name of the image. The convention to use the name
of the image to form the path to the layer data dates back tot he days when
Krita could save more than one image in a kra file. *Note that this is 
no longer supported.*

The image data directory contains three folders: ``layers``, ``palettes`` 
and ``annotations``.  The layers directory contains layer data, the 
palettes directory palettes (color sets) that are saved with the document
and the annotations directory contains in any case the ICC color profile
that is used for the image, and can contain other data as well.

The layer data consists of three files: ``layer``, ``layer.icc`` and ``layer.defaultpixel``.
The layer file contains compressed pixel data. The format of the pixel data
is internal to Krita and dependent on the version of Krita and can change 
without warning.

There are currently two compressors:

https://invent.kde.org/kde/krita/-/blob/master/libs/image/tiles3/swap/kis_tile_compressor_2.cpp

and the legacy compressor for reading older .kra files:

https://invent.kde.org/kde/krita/-/blob/master/libs/image/tiles3/swap/kis_legacy_tile_compressor.cpp

The ``layer.icc`` file contains the icc profile for the layer, even if it's
the same profile as used for the image. Krita .kra files can contain a heterogenous
layer stack, that is layers of different colorspaces can occur in the stack.

The ``layer.defaultpixel`` file contains a binary representation of a color
conforming to the layer's colorspace and defines the default color for pixels that
are not defined.



Vector layers are saved as SVG documents, in a further subfolder like ``layer2.shapelayer/content.svg``.

preview.png
~~~~~~~~~~~

An .kra file must have a ``preview.png`` in order to allow file
browser software to render the thumbnail efficiently. It must be a
non-interlaced PNG with 8 bits per channel of at most 256x256 pixels. It
should be as big as possible without upscaling or changing the aspect
ratio. Any aspect ratio is permitted. It should not contain any frame or
decoration.

The thumbnail file must not be referenced in any ``.xml`` file.

Optional Files
--------------

mergedimage.png
~~~~~~~~~~~~~~~

An .kra file can have a ``mergedimage.png`` in order to accommodate 
interoperability with viewer software and other application. It must 
contain the final rendered image without any frame or decoration. This 
file must be a PNG file with 8 or 16 bits per channel. Backup and 
autosave files do not have a mergedimage.png.

Layer Types
-----------

Krita supports a number of layer and mask types.

As shown in the example section, there's several bits of data that makes up a stored layer in Krita.

The first part is it's entry in the maindoc.xml. This is where things like visibility and layer blending mode are stored, as well as the position of the layer inside the layer stack.

colorlabel
    An integer determining the color label.
x
    The x offset in pixels.
y
    The y offset in pixels
onionskin
    Whether or not onionskins are enabled.
filename
    References the main file in the layer folder that holds the pixeldata or svg data of this layer.
locked
    Whether or not editing is enabled.
collapsed
    Whether or not child layers are visible in the docker.
opacity
    The opacity of the layer, running from 0 to 255
compositeop
    The composite operation, or blending mode of the layer
nodetype
    The type of layer a given layer is.
name
    The label assigned to this layer inside the layer docker. this is not unique.
colorspacename
    The model of the colorspace.
visible
    Whether or not the layer is visible.
selected
    Whether the layer was selected upon save.
uuid
    The unique identifier of this layer. Should always be unique.
intimeline
    Whether or not the layer is visible in the timeline.
channelflags
    Which channels are enabled.
channellockflags
    Which channels are locked for editing.
keyframes
    The filename of the keyframes


The second part is the 

Raster based layers
~~~~~~~~~~~~~~~~~~~

These include paint layers, transparency masks, selection masks, colorize masks and yes, filter layers, filter masks and fill layers.

Of these, only paint and colorize masks have pixel data in multiple channels, with the maximum amount of color channels being five, for CMYKA. For the other layers, the main pixeldata is the single-channel alpha color model, which determines where the mask or layer is active. These single channel layers will not have an associated icc profile embedded, but will have a defaultpixel file.

For filter layers, filter masks, and fill layers, the filter itself is stored as an xml configuration with the suffix 'filterconfig'.

Within the maindoc.xml, masks are always children of regular layer types.

::

    <layer collapsed="0" channelflags="" nodetype="clonelayer" clonetype="0" opacity="255" locked="0" name="Copy of cloneofcolumn" compositeop="normal" x="96" clonefrom="lowerpart" visible="1" colorlabel="0" filename="layer164" y="96" uuid="{9c2ad9b5-7430-4a5b-a1fb-04066eb549cf}" clonefromuuid="{004207ce-e03c-4994-966c-a690618e3555}">
          <masks>
           <mask nodetype="transparencymask" locked="0" name="Transparency Mask 1" x="32" visible="1" filename="mask165" y="0" uuid="{5022b0f4-65dd-4323-8090-55dafa78a662}"/>
          </masks>
         </layer>

With colorize masks, there's a seperate folder (mask#.colorizemask) holding all the layer data stored for each guidance color stroke (named 'keystroke_#') as well as the total calculated result of the colorize mask. Furthermore, there is a configuration file stored in the content.xml, sorting the strokes. Mask specific settings are in maindoc.xml
::

    <layer collapsed="0" visible="1" selected="true" compositeop="normal" nodetype="paintlayer" x="0" channellockflags="" filename="layer2" name="Layer 5 Merged" colorlabel="0" y="0" colorspacename="RGBA" opacity="255" locked="0" channelflags="" uuid="{83910f4f-c93d-41a4-856a-af5ec307a152}">
      <masks>
        <mask visible="1" fuzzy-radius="33.5" colorspacename="RGBA" name="Colorize Mask 1" use-edge-detection="1" y="-138" locked="0" limit-to-device="1" nodetype="colorizemask" compositeop="behind" edit-keystrokes="1" cleanup="70" x="466" show-coloring="1" uuid="{33fc243f-b24e-4e16-99f4-fed536283593}" filename="mask7" edge-detection-size="2"/>
      </masks>
    </layer>

use-edge-detection
    whether or not to use edge detection.
limit-to-device
    whether or not to limit the colorize area to the total layer size instead of the full canvas size.
cleanup
    strength of the cleanup.
show-coloring
    Whether or not the result is shown, corresponds to 'show output' in the ui.
edgedetectionsize
    strength of the edgedetection filter.
edit-keystrokes
    whether or not the editing of keystrokes is available.
fuzzy-radius
    corresponds to gap-close-hint.
    
The configuration file looks as follows:
::
    <!DOCTYPE doc>
    <colorize>
     <keystrokes type="array">
      <item_0 filename="keystroke_0" is-transparent="0" ColorData="9Z9j/w==" type="keystroke"/>
      <item_1 filename="keystroke_1" is-transparent="0" ColorData="88y6/w==" type="keystroke"/>
      <item_2 filename="keystroke_2" is-transparent="0" ColorData="Y1w9/w==" type="keystroke"/>
     </keystrokes>
    </colorize>

filename
    The name of the pixeldata file for a guiding stroke.
ColorData
    A 8bit sRGB representation of the stroke color, encoded in base64.
is-transparent
    Whether the stroke area is filled with a fully transparent color upon calculation.

Vector Layers
~~~~~~~~~~~~~

Vector layers are SVG files, which largely conform to the SVG 1.1 standard.

The following items are unique to Krita:

- something something markers.


Group Layers
~~~~~~~~~~~~

Group layers are groupings of other layers. They therefore only exist in the xml.

code::

    <layer collapsed="0" channelflags="1110" passthrough="0" nodetype="grouplayer" opacity="255" locked="0" name="shading" compositeop="hard_light" x="0" visible="1" colorlabel="0" filename="layer111" y="0" uuid="{fc5cef48-b073-41d9-99d7-0e98b42c106e}">
      <layers>
       <layer collapsed="0" channelflags="" nodetype="adjustmentlayer" opacity="255" locked="0" name="phongbumpmapfilter" filterversion="2" compositeop="normal" x="0" visible="1" colorlabel="7" filtername="phongbumpmap" filename="layer112" y="0" uuid="{e4a9012d-7f0b-4079-bc58-2574e9827774}"/>
       <layer collapsed="0" channellockflags="1111" channelflags="" nodetype="paintlayer" opacity="255" locked="0" colorspacename="RGBA" name="center Merged" compositeop="normal" x="0" visible="1" colorlabel="0" filename="layer113" y="0" uuid="{675de85e-e8fe-4759-b4b6-064ba8c0000a}"/>
       <layer collapsed="0" channellockflags="" channelflags="" nodetype="paintlayer" opacity="255" locked="0" colorspacename="RGBA" name="left-side-roof Merged" compositeop="normal" x="0" visible="1" colorlabel="0" filename="layer114" y="0" uuid="{7ba85939-2ca3-47b8-afc9-24c915ca48ea}"/>
       <layer collapsed="0" channellockflags="" channelflags="" nodetype="paintlayer" opacity="255" locked="0" colorspacename="RGBA" name="right-side-roof Merged" compositeop="normal" x="0" visible="1" colorlabel="0" filename="layer115" y="0" uuid="{d8eed159-fcca-48d0-9b35-900c5e6d1b68}"/>
       <layer collapsed="0" channellockflags="" channelflags="" nodetype="paintlayer" opacity="255" locked="0" colorspacename="RGBA" name="frontal Merged" compositeop="normal" x="0" visible="1" colorlabel="0" filename="layer116" y="0" uuid="{12d2dd09-1c49-4c36-98be-a6f28a15df5b}"/>
      </layers>
     </layer>

In the above xml, there is a group layer named 'shading', which has three paintlayers and a filter layer on top.

passthrough
    Whether or not passthrough compositing is enabled.

Clone Layers
~~~~~~~~~~~~

Clone layers intended to be instances of other layers. Therefore, clone layers only exist inside the maindoc.xml.

code::
    <layer collapsed="0" channelflags="" nodetype="clonelayer" clonetype="0" opacity="176" locked="0" name="Layer 15" compositeop="multiply" x="0" clonefrom="base" visible="1" colorlabel="0" filename="layer5" y="0" uuid="{d5bef0e8-a56d-468c-a4b1-3e2ee14b5ecf}" clonefromuuid="{6efa9638-73da-4d0e-87dc-987572c7f854}"/>


clonefrom
    name of the layer to cloen from.
clonetype
    ???
clonefromuuid
    the unique identifier of the layer to clone from.

File Layers
~~~~~~~~~~~

File layers refer to an image on disk, can dynamically update, and thus only exist in maindoc.xml.

::
    <layer uuid="{649eef83-f6d0-4a04-abdc-d4f50ff927f9}" colorlabel="0" locked="0" x="0" collapsed="0" name="Layer 2" colorspacename="RGBA" channelflags="" source="bluemorning_3_big.png" y="0" scale="false" scalingmethod="1" opacity="255" compositeop="normal" intimeline="1" visible="1" nodetype="filelayer" filename="layer3">
    
Source is the location of the referenced image via a relative path. If Krita cannot find the source, it will ask the user to reselect the image for it.

scale
    ???
scalingmethod
    how the file layer is scaled.

Transform Masks
~~~~~~~~~~~~~~~

::
    <masks>
     <mask locked="0" visible="1" x="0" nodetype="transformmask" uuid="{991f279d-fbf6-4e58-8c14-628573984eda}" filename="mask4" y="0" name="Transform Mask 1"/>
    </masks>

which then refers to mask4.transformconfig:

::

    <!DOCTYPE transform_params>
    <transform_params>
     <main id="tooltransformparams"/>
     <data mode="0">
      <free_transform>
       <transformedCenter type="pointf" x="1237.26259759923" y="2075.58428207406"/>
       <originalCenter type="pointf" x="1240" y="697.5"/>
       <rotationCenterOffset type="pointf" x="0" y="0"/>
       <transformAroundRotationCenter type="value" value="1"/>
       <aX type="value" value="0"/>
       <aY type="value" value="0"/>
       <aZ type="value" value="5.8985950918511"/>
       <cameraPos type="vector3d" z="1024" x="0" y="0"/>
       <scaleX type="value" value="0.669217242265994"/>
       <scaleY type="value" value="0.615848150006081"/>
       <shearX type="value" value="-0.606236132474432"/>
       <shearY type="value" value="0"/>
       <keepAspectRatio type="value" value="0"/>
       <flattenedPerspectiveTransform m12="0" m23="0" type="transform" m11="1" m33="1" m22="1" m32="0" m13="0" m21="0" m31="0"/>
       <filterId type="value" value="Bilinear"/>
      </free_transform>
     </data>
    </transform_params>

Guides, grids, assistants and other data
----------------------------------------

Outside of layers and their composition, Krita also stores a number of other things inside a kra file.

Grids
~~~~~

Only exist inside the maindoc.xml.

::

  <grid>
   <showGrid value="1" type="value"/>
   <snapToGrid value="1" type="value"/>
   <offset type="point" x="0" y="0"/>
   <spacing type="point" x="16" y="16"/>
   <offsetAspectLocked value="1" type="value"/>
   <spacingAspectLocked value="1" type="value"/>
   <subdivision value="2" type="value"/>
  </grid>

Mirror Axes
~~~~~~~~~~~

::

    <MirrorAxis>
        <mirrorHorizontal value="1" type="value"/>
        <mirrorVertical value="0" type="value"/>
        <lockHorizontal value="0" type="value"/>
        <lockVertical value="0" type="value"/>
        <hideHorizontalDecoration value="0" type="value"/>
        <hideVerticalDecoration value="0" type="value"/>
        <handleSize value="32" type="value"/>
        <horizontalHandlePosition value="107" type="value"/>
        <verticalHandlePosition value="64" type="value"/>
        <axisPosition y="1754" x="444.102203369141" type="pointf"/>
    </MirrorAxis>
  
Animation
~~~~~~~~~

In the maindoc.xml, the total length of animation is stored:

::

 <animation>
   <framerate value="8" type="value"/>
   <range to="12" from="0" type="timerange"/>
   <currentTime value="6" type="value"/>
  </animation>
  
framerate
    the fps.
range
    the range of the active animation area.
currentTime
    the selected frame upon save.

With the exception of the colorize mask, each of the raster based layers can have animation keyframes, which can be of the frame-by-frame type or the animation curves type (opacity only in this case). In both cases, there will be a layername.keyframes.xml file in the layers folder, which is referenced inside the maindoc.xml with the keyframes attribute:

::
   <layer onionskin="0" colorspacename="RGBA" intimeline="0" keyframes="layer2.keyframes.xml" filename="layer2" collapsed="0" nodetype="paintlayer" locked="0" channelflags="" colorlabel="0" opacity="255" compositeop="normal" channellockflags="1111" y="0" visible="1" name="Layer 9" uuid="{14ea94f7-faaf-48a7-b38e-e27537b614d2}" x="0"/>

The keyframes.xml file will look something like this:

::
        <?xml version="1.0" encoding="UTF-8"?>
        <!DOCTYPE keyframes PUBLIC '-//KDE//DTD krita-keyframes 1.0//EN' 'http://www.calligra.org/DTD/krita-keyframes-1.0.dtd'>
        <keyframes xmlns="http://www.calligra.org/DTD/krita-keyframes">
          <channel name="content">
            <keyframe color-label="0" time="0" frame="layer4">
              <offset y="0" type="point" x="0"/>
            </keyframe>
            <keyframe color-label="0" time="1" frame="layer4.f5">
              <offset y="-1" type="point" x="0"/>
            </keyframe>
            <keyframe color-label="0" time="2" frame="layer4.f6">
              <offset y="-2" type="point" x="0"/>
            </keyframe>
        
            -- snip --
            
            <keyframe color-label="0" time="12" frame="layer4.f18">
              <offset y="0" type="point" x="0"/>
            </keyframe>
          </channel>
          <channel name="opacity">
            <keyframe color-label="0" time="0" interpolation="bezier" value="77" tangents="sharp">
              <leftTangent y="0" type="pointf" x="0"/>
              <rightTangent y="3" type="pointf" x="3.16667"/>
            </keyframe>
            <keyframe color-label="0" time="6" interpolation="bezier" value="253.736" tangents="smooth">
              <leftTangent y="-0.0963729" type="pointf" x="-3.11309"/>
              <rightTangent y="0.106614" type="pointf" x="3.4439"/>
            </keyframe>
            <keyframe color-label="0" time="12" interpolation="bezier" value="77" tangents="smooth">
              <leftTangent y="0" type="pointf" x="-3.83333"/>
              <rightTangent y="0" type="pointf" x="0"/>
            </keyframe>
          </channel>
        </keyframes>
        
time
    the frame at which a given keyframe is placed.
color-label
    the color of the frame. This is the exact same list as the regular layer color labels, and these are often used to mark important parts of the animation.
frame
    the frame data file that a 'content' channel is pointing at. Note how the first frame points at the regular layer data, but subsequent frames are suffixed with 'f#' .
offset
    unique frame x/y offset. This gets added on top of the layer offset.

Animation curves are drawn from keyframe to keyframe. They can be visualized as having the time as the x-axis value and value as the y-axis value. The left and right tangent are then the extra nodes used for interpolation, in this case using bezier.

Assistants
~~~~~~~~~~


::
 <GlobalAssistantsColor SimpleColorData="176,176,176,255"/>
 <assistants>
   <assistant type="perspective" filename="perspective0.assistant"/>
  </assistants>
  
An assistant file will be stored under the assistants folder, and will look something like this:

::
    <?xml version="1.0" encoding="UTF-8"?>
    <assistant type="perspective">
      <handles>
        <handle id="0" x="904.497" y="673.939"/>
        <handle id="1" x="642.474" y="736.140"/>
        <handle id="2" x="362.778" y="663.851"/>
        <handle id="3" x="623.824" y="637.784"/>
      </handles>
    </assistant>


Guides
~~~~~~

::
  <guides>
   <showGuides type="value" value="0"/>
   <snapToGuides type="value" value="1"/>
   <lockGuides type="value" value="1"/>
   <horizontalGuides type="array">
    <item_0 type="value" value="70.866265639"/>
    <item_1 type="value" value="827.71799415"/>
    <item_2 type="value" value="28.346504912"/>
    <item_3 type="value" value="870.23764067"/>
   </horizontalGuides>
   <verticalGuides type="array">
    <item_0 type="value" value="57.6"/>
    <item_1 type="value" value="595.27662382"/>
    <item_2 type="value" value="28.346506553"/>
    <item_3 type="value" value="623.62310133"/>
   </verticalGuides>
   <rulersMultiple2 type="value" value="0"/>
   <unit type="value" value="px"/>
  </guides>


Proofing
~~~~~~~~

::

 <IMAGE description="" proofing-intent="3" width="2718" colorspacename="RGBA" name="Page 1" height="3747" mime="application/x-kra" y-res="300" profile="sRGB-elle-V2-srgbtrc.icc" proofing-adaptation-state="1" proofing-model="CMYKA" proofing-depth="U8" proofing-profile-name="Chemical proof" x-res="300">
 
 -- snip layers --
 
    <ProofingWarningColor>
      <RGB r="0.0039215688594" space="sRGB-elle-V2-srgbtrc.icc" b="0" g="1"/>
    </ProofingWarningColor>
  
  </IMAGE>
  
The proofing profile will be stored inside the annotations/proofing folder.

Layerstyles
~~~~~~~~~~~

Layer styles, when applied to a layer are referenced via a UUID.

::
    <layer channelflags="" opacity="255" uuid="{f6f4dd3f-8277-405c-84bf-e90c05893706}" x="109" y="127" name="panel1" filename="layer9" collapsed="1" intimeline="0" passthrough="0" nodetype="grouplayer" layerstyle="{6504ac26-78b7-47ea-9f1b-d36528b430df}" compositeop="normal" visible="1" colorlabel="0" locked="0">
    
The layerstyles themselves will be stored inside the layerstyles.asl file, in the annotations folder.

Reference Images
~~~~~~~~~~~~~~~~

::

    <layer nodetype="referenceimages">
      <referenceimage keepAspectRatio="true" transform="translate(39.1135888501742, 101.695331010453)" saturation="1" opacity="1" src="reference_images/0.png" width="152.542996515679" height="152.542996515679"/>
    </layer>

Reference images, weirdly enough, are not in the document name folder, instead they're top-level in the reference_images folder.

Projection Background
~~~~~~~~~~~~~~~~~~~~~

::
    <ProjectionBackgroundColor ColorData="oKu8/w=="/>

The projection background is an 8bit sRGB color encoded in base64. This is the color that is shown between the lowest of the layers and the transparency checkers.

Palettes
~~~~~~~~

::

    <palettes>
        <palette filename="flower_palette_embedded.kpl"/>
    </palettes>
    
The palettes are stored as KPL files as palettes/palete_name.kpl.
