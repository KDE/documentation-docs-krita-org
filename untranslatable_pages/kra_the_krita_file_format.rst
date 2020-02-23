.. meta::
    :description:
        Deswcription of the Krita File Format

.. metadata-placeholder

    :authors: - Boudewijn Rempt <boud@valdyas.org>
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
autosave files do not have a mergedimage.png/
