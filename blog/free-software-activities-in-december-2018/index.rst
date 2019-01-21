.. title: Free Software Activities in December 2018
.. slug: free-software-activities-in-december-2018
.. date: 2019-01-20 18:19:53 UTC-06:00
.. tags: debian
.. category: 
.. link: 
.. description: 
.. type: text

Hello again for another of my monthly updates on my work on Debian Science and
the FreeCAD ecosystem.

There's only a few announcement items since I was mostly enjoying my holidays,
but several important things were accomplished this month. Also, since there's
not much time left before the release of Debian 10, there's some consideration
to be done towards what I'll be working on in the next few months.

gmsh bugfix; no gmsh 4 yet
==========================
.. image:: /images/dec18-gmsh.png
  :align: center

At the beginning of the month, I uploaded gmsh 3.0.6+dfsg1-4. This had a patch
submitted by Joost van Zwieten (thanks!) to fix `Debian bug #904946
<https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=904946>`_ which was
preventing gmsh usage in FreeCAD, as well as adding an autopkgtest to make sure
that behavior remains.

New Coin3D transition; Pivy uploaded!
=====================================
.. image:: /images/dec18-coin3d.jpeg
  :align: center

Near the middle of the month, Leo Palomo-Avellaneda, Anton Gladky, and I finished the
transition for the coin3 package, which is a scene graph library and high-level
wrapper of OpenGL. The new version is a pre-release coin3 4.0.0 which adds
CMake support. It also fixes `Debian bug #874727
<https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=874727>`_ which caused
FreeCAD to segfault when importing an SVG.  FreeCAD also uses pivy, a Python
wrapper for coin, as a runtime dependency, and completing this transition has
finished the last blocker for a Python 3 FreeCAD package, so thanks to Leo and
Anton!

New release for med-fichier (not by me)
=======================================
.. image:: /images/dec18-HDF.svg
  :align: center

Another FreeCAD dependency had a new release this month, `med-fichier 4.0.0
<https://tracker.debian.org/pkg/med-fichier>`_.  This software is developed by
Électricité de France and built on the HDF5 library and file format but is
specialized for mesh data. It is also a dependency of gmsh which introduced
some difficulty for the gmsh package.

OpenFOAM upstream switch; from openfoam.org to openfoam.com
===========================================================
.. image:: /images/dec18-openfoam.jpg
  :align: center

The final noteworthy item for this month was an interesting bit of
correspondence I received concerning the OpenFOAM package. As I had mentioned
in previous posts, the current OpenFOAM version in Debian is 4.x, and I had
worked on updating the package for OpenFOAM 6.x. My packaging was working and
complete last summer, but for an inexplicable reason it stopped building late
summer, started building again for about a week in September, and then stopped
again. I would really like an up-to-date OpenFOAM in Debian 10, and so when I
received an email from the people at openfoam.com about packaging their
version, I was very intrigued. You see, the version in Debian is currently from
openfoam.org. Besides the TLD difference, there is a bit of history between the
two versions, but for end users there should major difference. If you're
interested in more background, you can consult `this video by József Nagy
<https://www.youtube.com/watch?v=8ggYvqEwghQ>`_.

Similarly, it seems likely that the OpenFOAM package will be changing over to
the openfoam.com version soon. I've already succesfully built the latest
OpenFOAM from this source, version 1812, and plan to submit it soon.

Thanks to my sponsors
=====================
This work is made possible in part by contributions from readers like you! You
can send moral support my way `via Twitter @thekurtwk
<https://twitter.com/thekurtwk>`_.  Financial support is also appreciated at
any level and possible on several platforms: `Patreon
<https://patreon.com/kkremitzki>`_, `Liberapay
<https://liberapay.com/kkremitzki>`_, and `PayPal
<https://paypal.me/kkremitzki>`_.
