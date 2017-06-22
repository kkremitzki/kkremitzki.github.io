.. title: GSoC Week 2 recap
.. slug: gsoc-week-2-recap
.. date: 2017-06-18 18:40:33 UTC-05:00
.. tags: gsoc,freecad
.. category: 
.. link: 
.. description: 
.. type: text

With the four major bugs blocking the usage of ``PartDesign Mirrored`` fixed, 
I started out the week exploring the now-functioning tool with the goal of getting what I call "command test coverage". 
In short, this means testing major variations for tools presented to the user in the PartDesign WB. 

For reference, they are depicted and categorized in figures 1 and 2, 
with the newly redesigned icons made by `Alexander Gryson <https://github.com/agryson>`_ (kudos to his major rework of all of FreeCAD's icons!)

.. figure:: /images/gsoc-2-1.png
  :width: 900
  :align: center
  :alt: command palette

  Figure 1. Datum tools, additive/subtractive features and primitives.

.. figure:: /images/gsoc-2-2.png
  :width: 600
  :align: center
  :alt: command palette

  Figure 2. Transformations, dressup features, and multi-body boolean operation.


The Mirrored tool takes as input feature(s) and a mirror plane, but the other transformation tools like LinearPattern and PolarPattern behave in a fundamentally similar way. 
By that reasoning, I figured that tests regarding the Mirrored tool really only have two major permutations if one assumes valid input: 
the case where a choice of features and plane succeeds, and one where it doesn't.

.. figure:: /images/gsoc-2-3.png
  :width: 600
  :align: center
  :alt: mirrored success

  Figure 3. Success!


.. figure:: /images/gsoc-2-4.png
  :width: 600
  :align: center
  :alt: mirrored failure

  Figure 4. Failure...


So, I cleaned up the test case submission I started GSoC out with, ``testMirroredSketchCase``, 
and added the new case depicted in figure 4, ``testMirroredOffsetFailureCase``.
However, I noticed both of my test cases involved ``Sketch``-based additive features, but no additive primitives.
So, I also included ``testMirroredPrimitiveCase`` in `FreeCAD PR#816 <https://github.com/FreeCAD/FreeCAD/pull/816>`_.

What's nice is that besides ``PartDesign Mirrored`` now being fixed, several other transformation tools' bugs were resolved.
Altogether, the PR resolved four issues, `2235 <https://www.freecadweb.org/tracker/view.php?id=2235>`_, 
`2248 <https://www.freecadweb.org/tracker/view.php?id=2248>`_, `3006 <https://www.freecadweb.org/tracker/view.php?id=3006>`_,
and `3065 <https://www.freecadweb.org/tracker/view.php?id=3065>`_.

With all that wrapped up, 
I moved on to adding tests for the various options for the fundamental sketch-based features ``Pad`` and ``Pocket``.
Altogether, I added ``testPadToFirstCase``, ``testPadtoLastCase``, ``testPadToFaceCase``,
and ``testPadTwoDimensionsCase`` to cover the options for ``PartDesign Pad``. 
Unfortunately, these test cases are not very interesting to look at and mostly involve 2-4 lined up cubes similar to
what figure 3 looks like.

However, for ``PartDesign Pad``, things do get a little more interesting. 
The base case is a simple reversed pad with a pocket in the middle, shown in figure 5.

.. figure:: /images/gsoc-2-5.png
  :width: 600
  :align: center
  :alt: mirrored failure

  Figure 5. The base Pocket test construction.

It was straightforward to add ``testPocketDimensionCase``, ``testPocketThroughAllCase``,
and ``testPocketToFirstCase``. 
However, covering the last Pocket option with ``testPocketToFaceCase`` is not (necessarily) so trivial.

If you refer to figure 5, you'll note that the base Pad feature is a hexahedron, or six-sided shape.
The Pocket feature adds four new faces to the overall shape, ``Face7`` through ``Face10``. 
However, references relying on the numbering of those faces is inherently brittle and is being addressed
by another one of the GSoC projects this year.
Because of that, I'll give a little bit more thought on how to construct the test before proceeding.
