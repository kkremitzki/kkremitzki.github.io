.. title: Halloween Update for FreeCAD & Debian Science Work
.. slug: halloween-update-for-freecad-debian-science-work
.. date: 2019-10-31 22:04:54 UTC-05:00
.. tags: debian,freecad
.. category: 
.. link: 
.. description: 
.. type: text

There's been a spooky amount of activity in the FreeCAD & Debian Science world
since I last wrote!  Because this update covers August, September, and October,
I'll try to be brief and only touch on the key points.

.. contents::


Staging & Merging App::Link Functionality
=========================================


.. figure:: /images/applink.png
  :width: 600
  :align: center
  :alt: App::Link example

  *The "App::Link" object allows lightweight linking of objects in a document
  and from external documents.*


In August, a major milestone towards unified, mainline mechanical assembly
functionality in FreeCAD was reached. 

One of the core challenges in implementing assembly functionality is the
problem of topological naming. In a CAD model there are topological entities,
such as solids, faces, edges, and vertices. We must choose some algorithm to
name them so that you can refer to relationships to make an assembly. A simple
example would be two cubes, connected by touching faces. If a parameter in your
model changes, and after recalculation, your "Face_N" is on the wrong side of
the cube, your assembly may break, or not be what you are expecting. Without a
good approach to topological naming, parametric FreeCAD models won't be robust
to changes and recalculations, which defeats the purpose of parametric
modeling.

Because this is such a difficult problem, progress has been slow. However,
recently a relatively new FreeCAD developer, 'realthunder', put significant
work towards this problem, with a solution finally on the horizon. Because it
required major changes to FreeCAD's internals, the review and testing period
was and continues to be lengthy.

The milestone in particular was merging of a large chunk of this code, referred
to in short as "App::Link functionality". This diff is huge: *+70,441*
*-14,562* lines of C++. You can `read more about it on the pull request itself
<https://github.com/FreeCAD/FreeCAD/pull/2350>`_.

I only played a minor contributing role in this effort, preparing a short-lived
staging PPA to provide a package for testers after the pull request was opened
in July, but it's rather significant news in terms of the project and so worth
spreading. Mechanical assembly is (no surprise) a must-have for mechanical
engineers interested in FreeCAD, and it's considered by some to be the last
remaining blocker for FreeCAD's 1.0 release.

Extra links: notes for code reviewers from the PR author, for the dedicated
readers out there.

* https://github.com/realthunder/FreeCAD_assembly3/wiki/Concepts
* https://github.com/realthunder/FreeCAD_assembly3/wiki/Core-Changes

FreeCAD Python 2 removal in Debian Testing
==========================================
The Python 2 removal in Debian Testing continues, and with it, FreeCAD's Python
2 package is gone. However, upon upload, several new build failures appeared on
the i386, mipsel, and s390x platforms. Turns out there was a regression in dwz,
a software I had never heard of before. I tried troubleshooting but
unfortunately had FreeCAD drop out of testing due to the Python 2 removal bug
filed against it.

Luckily, when I `filed a bug against dwz
<https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=942193>`_, Matthias Klose
and Tom de Vries helped isolate and upstream the problem, with Tom even
`bisecting the regressing commit in the upstream bug
<https://sourceware.org/bugzilla/show_bug.cgi?id=25109>`_. Thank you, you two!

After adding a workaround to fix those build failures, the new Python 3-only
FreeCAD package is on its way to Debian Testing.

FreeCAD Python 3 support added for Ubuntu 16.04
===============================================
Qt 5 & Python 3 builds for FreeCAD have been available on Ubuntu 18.04 and
newer and Debian 10 and newer platforms for some time now. However, Ubuntu
16.04 was problematic due to its old Qt version, which meant a Qt 4, Python 3
build had to be produced. This had been on the back burner for a while because
when I initially attempted backporting the necessary packages, I encountered
some friction.

However, since it's the last holdout Python 2 platform, I took another look at
things to try to speed up the "py2ectomy". It turns out that the missing
package needed for a Python 3 build, pivy, was failing to build because of
`"PIE hardening"
<https://wiki.debian.org/Hardening#DEB_BUILD_HARDENING_PIE_.28gcc.2Fg.2B-.2B-_-fPIE_-pie.29>`_,
a Debian security hardening flag. I had all such flags turned on, so I just had
to disable that particular one to get things going.

So, Python 3 builds are now available for Ubuntu 16.04 in the `FreeCAD Daily
Builds PPA
<https://launchpad.net/~freecad-maintainers/+archive/ubuntu/freecad-daily>`_,
and they will be coming soon to the stable PPA as well. A new bugfix release
has been made for stable, 0.18.4, so I am working on that first, and the Python
3 package will come with it.

Netgen and Pybind11 Builds
==========================
Good news for users of FreeCAD's finite element modeling workbench!

Integration with Netgen, a mesh generator, has long been an optional but
off-by-default build option for FreeCAD, due to packaging difficulties.
However, since I have taken over things in recent years, I have finally gotten
things to the state where we can turn this back on by default. As part of this
change, I am also building FreeCAD with Pybind11 instead of Boost.Python,
marking another milestone in managing FreeCAD's dependencies.

Since this may introduce bugs, I've started by making this change for all of
FreeCAD's daily builds in the Ubuntu PPA, as well as the package currently in
Debian Unstable. Eventually, this change may come to the stable PPA.

OpenCASCADE 7.4.0
=================

.. figure:: /images/occt740.png
  :width: 600
  :align: center
  :alt: OCCT performance improvement example

  *An assembly of a single solid box replicated ~93,000 times. This test case is more than 10x faster in OCCT 7.4.0.*


`After more than a year of development
<https://www.opencascade.com/sites/default/files/documents/release_notes_7.4.0.pdf>`_ (PDF warning), a new
minor version of OpenCASCADE Technology (OCCT) has been released.

OCCT is the geometry & topology kernel of FreeCAD, and it is also a dependency
for several related projects including Gmsh, IFCOpenShell, Netgen, and
OpenCAMLib. New releases in OCCT generally herald stability and performance
upgrades for core behavior. However, there are some breaking changes and so
these improvements are yet to be seen.

For the time being, OCCT 7.4.0 packages are available in `my OpenCASCADE PPA
<https://launchpad.net/~kkremitzki/+archive/ubuntu/opencascade>`_ and by
building the package directly from
https://salsa.debian.org/science-team/opencascade.

OpenFOAM 1906
=============
I uploaded `the latest version of OpenFOAM
<https://openfoam.com/releases/openfoam-v1906/index.php>`_, the toolbox for
computational fluid dynamics. It's now available in Ubuntu 19.10, Debian
Testing, and via the `FreeCAD Community Extras PPA
<https://launchpad.net/~freecad-community/+archive/ubuntu/ppa>`_.

Gmsh 4.4.1
==========
`The latest version of Gmsh
<https://gitlab.onelab.info/gmsh/gmsh/blob/master/CHANGELOG.txt>`_, a 3D finite
element mesh generator, is also in Ubuntu 19.10, Debian Testing, and the
Community Extras PPA. Thanks to Nico Schlömer for helping maintain this
package.

Netgen 6.2.1905
===============
This version of Netgen is only available via the FreeCAD Daily and Community
Extras PPAs. Unfortunately Netgen has been stuck in the Debian NEW queue for
over 8 months now.

GitHub Sponsors Program
=======================
I was accepted into the `GitHub Sponsors
<https://github.com/sponsors/kkremitzki/>`_ program! GitHub is matching
donations for the first year. Hopefully this helps fund my FOSS work, and FOSS
work in general.

Thanks for your support
=======================
I appreciate any feedback you might have.

You can get in touch with me `via Twitter @thekurtwk
<https://twitter.com/thekurtwk>`_.

If you'd like to donate to help support my work, `there are several methods
available on my site <https://www.kwk.systems/blog/pages/donate/>`_.
