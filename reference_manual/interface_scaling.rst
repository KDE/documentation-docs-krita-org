.. meta::
   :description property=og\:description:
        How to change the scale of Krita's interface on Android.

.. metadata-placeholder

   :authors: - Carsten Hartenfels
   :license: GNU free documentation license 1.3 or later.
   
.. _interface_scaling:

=================
Interface Scaling
=================

Krita's interface scale will automatically use the scaling of your screen set in your operating system. You can disable this behavior via the :ref:`hi_dpi_support` setting.

You can also force a specific interface scale by setting the ``QT_SCALE_FACTOR`` environment variable. A value of ``1`` means 100%, ``1.5`` is 150% and so on. Values below 100% are unsupported.

Android Interface Scale
=======================

On Android, you will be prompted to adjust the interface scale when Krita starts. Change the slider to make the interface larger and smaller. 100% is the minimum, you can't make it smaller than that.

After you saw it once, Krita will show you the option to disable the dialog on startup. The option doesn't appear the first time around to make sure you have a way out of setting a wrong scale by closing and reopening Krita.

You can bring back the dialog manually via :menuselection:`Settings --> Change Interface Scale...` in the top menu bar.

If you turn off the :ref:`hi_dpi_support` setting, the dialog will not be available until  you re-enable the setting and restart Krita.

    .. image:: /images/android_scaling_dialog.jpg
