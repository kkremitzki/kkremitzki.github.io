.. title: GSoC Week 8 Recap
.. slug: gsoc-week-8-recap
.. date: 2017-08-04 03:19:02 UTC-05:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text

Total tool coverage lasted less than a week! It's a good thing though, because that means a new tool `landed in master <https://github.com/FreeCAD/FreeCAD/pull/898>`_: PartDesign Hole.

.. image:: /images/PartDesign_Hole.svg
  :align: center
  :alt: Part Design Hole tool

This is a really great tool for the Part Design WB not only because holes (and their corresponding fasteners) are ubiquitous in part design generally,
but also because the tool does a good job of capturing that information into a FreeCAD object that can be later be hooked into for both the
Assembly and TechDraw workbenches. For example, the options I've selected in the following screenshot could be used to complete a technical drawing
for this part in FreeCAD, and that information exchange could be done in an automated and customizable way.

.. image:: /images/gsoc-8-1.png
  :align: center
  :alt: Part Design Hole tool

This information could also be used by the Path WB to generate control code for open-source, automated manufacturing processes and machines, so it's really
great to have such a full-featured tool added.

I spent some time trying to find bugs in the tool, but didn't really find any. The only gotcha I noticed is related to the orientation of sketches which serve as the
basis for holes. There is no Reverse option for the Hole feature itself, so for example, if you have a sketch on the "bottom" of an object but not attached to it,
you may need to set the Map Reversed option for the sketch itself to true.

Some tests will be forthcoming for Hole, but besides that, I also spent some time looking at few outstanding bugs in C++-land. 

Particularly,

- (mentioned in week 5) ShapeBinder crash when base object not initially selected due to null pointer dereference
- (mentioned in week 3) Revolution has unhandled error for some bad revolution axis choices, does bad revolution without error for others
- (new) Pipe fails when its path is a loop. For example, a Pipe with a circle as a base and a larger, orthogonal circle passing through the base should become a torus.
  Currently, it fails with the wonderfully verbose error message 'TopoDS::Shell'.
