.. title: Keeping zoom level when navigating PDF in Evince, GNOME's Document Viewer
.. slug: keeping-zoom-level-when-navigating-pdf-in-evince-gnomes-document-viewer
.. date: 2016-04-24 16:51:08 UTC-05:00
.. tags: linux
.. category: 
.. link: 
.. description: 
.. type: text

This one is short, sweet, and to the point. How often do you have your PDF set to a nice zoom level, only to have it reset when navigating via the Bookmarks/Index? If you use GNOME as a Linux DE (desktop environment), then you can fire up a terminal and use this ``gsettings`` one-liner to preserve zoom:

.. code-block:: bash

 gsettings set org.gnome.Evince allow-links-change-zoom false 

A great alternative PDF reader is the ``vim``-key friendly `zathura
<https://pwmt.org/projects/zathura/>`_. I've had issues opening larger PDFs with it though, so your mileage may vary.
