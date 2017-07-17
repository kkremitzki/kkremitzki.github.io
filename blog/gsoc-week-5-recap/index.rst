.. title: GSoC Week 5 recap
.. slug: gsoc-week-5-recap
.. date: 2017-07-11 14:45:35 UTC-05:00
.. tags: gsoc,freecad
.. category: 
.. link: 
.. description: 
.. type: text

This week started out with some interesting discussions on the future Python structure of FreeCAD, over
`on the forums <https://forum.freecadweb.org/viewtopic.php?f=10&t=23197>`_. This was especially salient
as I have a bit of pain interacting with parts of the FreeCAD Python API and improvements to it would
be a good long-term goal after finishing GSoC.

I decided that the ``TestPartDesignApp.py`` file I had been working in thus far needed splitting up,
as I was cramming almost every new test into it. 
The `new version of this file <https://github.com/FreeCAD/FreeCAD/blob/master/src/Mod/PartDesign/TestPartDesignApp.py>`_ 
is a pretty nice indicator of the overall status of PartDesign test coverage.

I also added some basic tests for datum tools, covering simple creation scenarios. While exploring the 4th datum
tool, ``ShapeBinder``, I found a bug that causes a crash, so I will need to look into that shortly to see if it's an
easy fix.

``LinearPattern`` and ``PolarPattern`` got 6 new tests each, covering all the major variations of sketch-
or primitive-based features.

Here's the pull request summarizing my work: https://github.com/FreeCAD/FreeCAD/pull/869

+----------------------------------+-----------------------------+-----------+-----------------------------+
| tool category                    | initial, current test count |  status   | notes                       |
+==================================+=============================+===========+=============================+
|  datum tools                     |            0, 3             |   ready   | found shapebinder crash bug |
+----------------------------------+-----------------------------+-----------+-----------------------------+
|  add. & sub. features/primitives |           15, 15            |   ready   |                             |
+----------------------------------+-----------------------------+-----------+-----------------------------+
|  transformations                 |            3, 15            |   ready   | all done but MultiTransform |
+----------------------------------+-----------------------------+-----------+-----------------------------+
|  dressup features                |            0, 4             |   ready   |                             |
+----------------------------------+-----------------------------+-----------+-----------------------------+
|  boolean operation               |            0, 0             |   ready   |                             |
+----------------------------------+-----------------------------+-----------+-----------------------------+
