.. title: GSoC Week 12: Final Work Product
.. slug: gsoc-week-12-final-work-product
.. date: 2017-08-27 12:50:18 UTC-05:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text

Well, it's time to finally wrap up the summer!

It's been a really great and rewarding opportunity, so I first want to thank everyone at Google and beyond who helped put GSoC together,
as well as my mentor Stefan Tröger for providing feedback and guidance.

I was able to work with code that ranged almost the entire stack of FreeCAD dependencies: from low-level OpenCASCADE code involving
quaternions & transformations, geometry & topology; to the scene graph library Coin3D we have to thank for our pretty screenshots;
the connection between C++ and Python code, which I have a feeling will be useful later in my engineering career; and all the way up to the
Qt GUI in both C++ as well as its Python interface PySide.

As a result, I feel very prepared to continue working with the FreeCAD project and look forward to doing so. I really think it's a great
program and hope to use it for many years in the future.

So again, my thanks!

The main goal of the project was to get test coverage of the Part Design Workbench, and to explore it to find showstopping bugs. The only 
remaining one involves a crash in ShapeBinder, discussed at https://freecadweb.org/tracker/view.php?id=2517.

I fixed quite a few bugs and I think the general experience with the workbench is better. 
Test coverage is there for all the tools, and I'd say the workbench is ready for the public, so now the major work is to release FreeCAD 0.17, 
the biggest FreeCAD release ever, with its new Part Design (no longer "NEXT") Workbench.

My other goal of improvements to Boolean Operation was made unnecessary by someone else's PR in May.

The last goal, improvements to the Attachment Editor, ended up being a little too big for this GSoC, and could even possibly serve
as a good GSoC project for next summer, although whoever does it had better be fairly artistic at making explanatory yet small icons.

In my opinion, I'd say the summer was a success.

Altogether, my code contribution can be summarized with 7 PRs and one experimental branch:

PR's:

1. https://github.com/FreeCAD/FreeCAD/pull/816
2. https://github.com/FreeCAD/FreeCAD/pull/829
3. https://github.com/FreeCAD/FreeCAD/pull/848
4. https://github.com/FreeCAD/FreeCAD/pull/869
5. https://github.com/FreeCAD/FreeCAD/pull/899
6. https://github.com/FreeCAD/FreeCAD/pull/920
7. https://github.com/FreeCAD/FreeCAD/pull/957

Experimental Attachment Editor/PartDesign Datum Tools branch:

- https://github.com/kkremitzki/freecad/tree/pdn_datum_tools

Here's my summary posts, summarized:

1. `</blog/gsoc-week-1-recap/>`_
2. `</blog/gsoc-week-2-recap/>`_
3. `</blog/gsoc-week-3-recap/>`_
4. `</blog/gsoc-week-4-recap/>`_
5. `</blog/gsoc-week-5-recap/>`_
6. `</blog/gsoc-week-6-recap/>`_
7. `</blog/gsoc-week-7-recap/>`_
8. `</blog/gsoc-week-8-recap/>`_
9. `</blog/gsoc-week-9-recap/>`_
10. `</blog/gsoc-week-10-recap/>`_
11. `</blog/gsoc-week-11-recap/>`_
