.. title: GSoC Week 7 Recap
.. slug: gsoc-week-7-recap
.. date: 2017-07-28 15:30:58 UTC-05:00
.. tags: 
.. type: text
.. has_math: yes

I hit a nice milestone this week! With `PR 899 <https://github.com/FreeCAD/FreeCAD/pull/899>`_ I hit total tool *test* coverage for the Part Design workbench.
Now, what exactly does that mean? Well, if you look at my screenshot of the workbench tools from Week 2, every one of those is now covered by tests with most
key functionality hit. Some of them, like the dressup features Fillet and Chamfer, only have one test, either because the tool is simple or because further tests
lie outside the scope of the Part Design workbench (e.g. testing the topological naming robustness of Fillet to recalculation.)

The PartDesign Primitive (Box, Cylinder, Sphere, Cone, Ellipsoid, Torus, Prism, and Wedge) tests were interesting to write. 
I was able to cover basic construction of both Additive and Subtractive primitives of each type by simply making a large Additive Primitive
and smaller Subtractive Primitive inside the first, and then ensuring that the ensuing Shape's Volume property was about equal to
the difference in volumes according to the formula for that shape, e.g. 

\\[
\\mathrm{Shape.Volume}\\ \\approx V = \\frac{4}{3}\\pi (R^3 - r^3)
\\]

for Additive-:math:`R` and Subtractive-:math:`r` Primitive Spheres. 
I had to look up a few volume formulas but otherwise the tests for the lengthly list in the parentheses above went quickly.

I also fixed a bug with Loft sections not being hidden, so e.g. the Sketches being lofted to or through were still visible.

Additionally, there was an issue with both Loft and Pipe not claiming children correctly in the tree which I fixed.
