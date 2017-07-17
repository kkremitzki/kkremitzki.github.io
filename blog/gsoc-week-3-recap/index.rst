.. title: GSoC Week 3 recap
.. slug: gsoc-week-3-recap
.. date: 2017-06-22 11:15:49 UTC-05:00
.. tags: gsoc,freecad
.. category: 
.. link: 
.. description: 
.. type: text

Howdy! I wasn't sure of the best way to represent my progress thus far, but I figure a table is an alright way to summarize.

+----------------------------------+-----------------------------+-----------+-----------------------------+
| tool category                    | initial, current test count |  status   | notes                       |
+==================================+=============================+===========+=============================+
|  datum tools                     |            0, 0             |   hold    | waiting on attachment       |
|                                  |                             |           | editor work in phase 2      |
+----------------------------------+-----------------------------+-----------+-----------------------------+
|  add. & sub. features/primitives |            3, 11            |  blocked  | basic Pipe not working; when|
|                                  |                             |           | fixed, all tools in this    |
|                                  |                             |           | category (but not all their |
|                                  |                             |           | options) will have test     |
|                                  |                             |           | coverage                    |
+----------------------------------+-----------------------------+-----------+-----------------------------+
|  transformations                 |            0, 3             |   ready   | Mirrored added, still need  |
|                                  |                             |           | Linear and PolarPattern     |
+----------------------------------+-----------------------------+-----------+-----------------------------+
|  dressup features                |            0, 0             |   ready   |                             |
+----------------------------------+-----------------------------+-----------+-----------------------------+
|  boolean operation               |            0, 0             |   ready   | Previously seemed to        |
|                                  |                             |           | misbehave but recent changes|
|                                  |                             |           | to containers may have fixed|
|                                  |                             |           | this                        |
+----------------------------------+-----------------------------+-----------+-----------------------------+

I got my Pad & Pocket tests added, so right now the total Δtests is 11. Next up is Loft and Pipe. However,
Pipe has a bit of a blocking bug right now. My test scenario involves a simple circle centered at the origin
in an XY-attached sketch, serving as the base Profile, and a simple line on the Z axis in an XZ-attached sketch.
The test construction is illustrated in figure 1.

This should result in a cylinder, as the preview indicates in figure 2. For some reason, when clicking OK,
an external reference warning is being generated, and this is blocking any test constructions for PartDesign Pipe.

.. figure:: /images/gsoc-3-3.png
  :width: 300
  :align: center
  :alt: test pipe construction

  Figure 1. PartDesign Pipe Profile and Spine sketches which should form a simple cylinder.


.. figure:: /images/gsoc-3-4.png
  :width: 600
  :align: center
  :alt: external reference warning

  Figure 2. PartDesign Pipe erroneously warning about external references.


I also ran into a bug in PartDesign Revolve, which, as bugs are wont to do, ended up being two bugs.
The construction case to see them is depicted in figure 3.

.. figure:: /images/gsoc-3-1.png
  :width: 300
  :align: center
  :alt: revolution sketches

  Figure 3. Simple sketches attached to the three base planes.

I attached a simple circle sketch to each of the three base planes, and offset them so they wouldn't be symmetric
with respect to the origin or any base axes. When attempting to add a Revolution with these sketches, they behave
as expected, until one attempts to revolve them about the axis which is normal to the sketch's plane. For the
XY- and YZ-attached sketches, the following error appears:

    Unhandled Base::Exception caught in GUIApplication::notify.
    The error message is: Rotation axis must not be perpendicular with the sketch plane

However, if one tries to revolve the XZ-attached circle, FreeCAD gives it the ol' college try, but
ends up with an awfully thin "solid":

.. figure:: /images/gsoc-3-2.png
  :width: 300
  :align: center
  :alt: faulty revolution

  Figure 4. An "error-free" PartDesign Revolution.


I'll also be looking into these bugs this week.
