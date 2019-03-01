.. title: My Free Software Activities in January & February 2019
.. slug: my-free-software-activities-in-january-february-2019
.. date: 2019-03-01 00:10:43 UTC-06:00
.. tags: debian,freecad
.. category: 
.. link: 
.. description: 
.. type: text

Intro
=====

Hello all and welcome again to another of my monthly summary posts on my work
in free software, with a focus on open engineering in `Debian
<https://www.debian.org/>`_ & `Ubuntu <https://www.ubuntu.com/>`_.  I'm
fortunate to have the `February 12th Debian 10 soft freeze deadline
<https://lists.debian.org/debian-devel-announce/2019/02/msg00008.html>`_ to
scapegoat for my missed January update, and thanks too to February for being
short enough to postpone it further and combine the two updates.

I've decided to go with a bit of a dryer chronological approach to this update
as there's lots to cover. Worth highlighting, however:

Highlights
==========

* New Debian upload for a `FreeCAD <https://www.freecadweb.org/>`_ 0.18 pre-release
* New Debian upload for `OpenFOAM <https://www.openfoam.com/>`_. An upstream
  switch from openfoam.org to openfoam.com and a different versioning scheme
  results in a massive version bump, 4.1 to 1812. That's over 1800 versions better.
  (Seriously though, it's about a 2 year bump in changes.)
* New Debian uploads for `mesh generation
  <https://en.wikipedia.org/wiki/Mesh_generation>`_ softwares `Gmsh
  <http://gmsh.info/>`_ 4.1.3 and `Netgen <https://ngsolve.org/>`_ 6.2.1810 --
  though Netgen might miss Debian 10? It's stuck in the NEW queue.
* FreeCAD is participating in Google Summer of Code and I'm looking for a
  student to mentor

----

Timeline
========

January
-------

* Jan 6: `Updated
  <https://forum.freecadweb.org/viewtopic.php?f=8&t=25175&start=20#p278504>`__
  the `FreeCAD bug tracker <https://freecadweb.org/tracker>`_ to the latest
  version.

* Jan 12: Completed transition of FreeCAD PPAs to new versions of `Coin3D
  <https://en.wikipedia.org/wiki/Coin3D>`_ & its Python bindings package Pivy,
  which `resolved a major breakage caused by me on Dec 29
  <https://forum.freecadweb.org/viewtopic.php?f=8&t=26599>`_ but was a necessary
  precursor to a FreeCAD 0.18 release; I just didn't execute it as well as I
  should have

* Jan 16: `Upload
  <https://tracker.debian.org/news/1021265/accepted-openfoam-1812dfsg1-1exp1-source-into-experimental/>`__
  of OpenFOAM 1812.

* Jan 18: `Discussed on GitHub
  <https://github.com/aewallin/opencamlib/issues/31#issuecomment-455452094>`_
  with the upstream of `OpenCAMLib <http://www.anderswallin.net/cam/>`_ about
  release plans now that it is Python 3 compatible

* Jan 19: `Contact via GitHub issue
  <https://github.com/libMesh/libmesh/issues/2003>`__ with `libMesh
  <http://libmesh.github.io/>`_ upstream about Debian packaging, with
  enthusiastic response. 

* Jan 19: `FreeCAD pull request
  <https://github.com/FreeCAD/FreeCAD/pull/1916>`_ to fix Start Workbench
  behavior in Debian/Ubuntu since we can't include binary `.FCStd
  <https://www.freecadweb.org/wiki/File_Format_FCStd>`_ examples, even though
  they're glorified ZIPs, for Debian Free Software Guidelines reasons (or can we?
  please contact me if you know otherwise)

* Jan 25-27: Hosted `Austin Debian Bug Squashing Party
  <https://wiki.debian.org/BSP/2019/01/us/Austin>`_. Unfortunately, it wasn't
  very successful in drawing in people besides those already interested in Debian
  at the host venue, the `ATX Hackerspace <http://atxhs.org/wiki/Main_Page>`_. I
  didn't want to over-advertise it since the venue was limited in capacity, which
  in retrospect was a mistake. Oh well, there was also plenty to learn for the
  next one. The following bugs were closed: 918479, 888026, 884092, 886538,
  882510, 899099, 920525, 919711.

* Jan 26: `Announced
  <https://forum.freecadweb.org/viewtopic.php?f=8&t=26599>`__ the experimental
  `staging.freecad.io <https://staging.freecad.io>`_, an instance of FreeCAD's
  homepage designed to test possible improvements to be had by moving away from
  shared hosting

* Jan 28: `Contact via GitHub issue
  <https://github.com/sfepy/sfepy/issues/496>`__ with `sfepy
  <http://sfepy.org/doc-devel/index.html>`_ upstream about it failing to build
  from source to try to get help on issue potentially preventing it from being
  included in Debian 10.

February
--------

* Feb 4: Sponsored uploads of `FreeCAD 0.18 pre-release
  <https://tracker.debian.org/news/1027009/accepted-freecad-018pre1dfsg1-1exp1-source-all-amd64-into-experimental-experimental/>`_
  and `Gmsh 4.1.3
  <https://tracker.debian.org/news/1027010/accepted-gmsh-413ds1-1-source-amd64-all-into-unstable-unstable/>`_
  into Unstable, thanks Anton Gladky.

* Feb 4: Announced `tracker.freecad.io <https://tracker.freecad.io>`_, an
  experimental instance of FreeCAD's bug tracker designed to test possible
  improvements to be had from moving away from shared hosting

* Feb 5: Regained control of abandoned FreeCAD Snap, which was a pre-release of
  0.17, by way of the uploader returning from MIA and adding me. 

* Feb 9: `Merge PR <https://github.com/FreeCAD/FreeCAD-Homepage/pull/33>`_ for
  FreeCAD-Homepage repo to add Expires headers and unset ETags to try to get
  better performance

* Feb 13: `Confirmed sfepy upstream fix resolved the issue
  <https://github.com/sfepy/sfepy/issues/496#issuecomment-463089344>`_, but it
  came a day after the soft freeze preventing re-entry to Testing.
  
* Feb 23: `Upload
  <https://tracker.debian.org/news/1031845/accepted-python-fluids-0173-1-source-into-unstable/>`__
  of python-fluids 0.1.73, experiment with `Salsa GitLab CI
  <https://salsa.debian.org/salsa-ci-team/pipeline/blob/master/README.md>`_.

* Feb 25: `Google Summer of Code <https://summerofcode.withgoogle.com/>`_
  organizations announced. FreeCAD participating under umbrella organization
  OpenCAx led by `BRL-CAD <https://brlcad.org/>`_. I created a `GitHub issue
  <https://github.com/opencax/GSoC/issues/13>`_ for the project I'd like to
  mentor. I'm looking for a student interested in improving the state of Debian &
  Ubuntu packaging for FreeCAD and its ecosystem of packages. Particularly -- not
  everyone's first encounter with FreeCAD is with the latest and greatest
  version. If someone installs an old version and has a bad experience with an
  easily fixable packaging bug, we should try to tackle that issue to not drive
  away people who are already interested, but get a bad impression.

* Feb 25: Sponsored `upload
  <https://ftp-master.debian.org/new/netgen_6.2.1810+dfsg1-1.html>`__ of Netgen to
  Unstable, thanks Anton Gladky. Netgen had to re-enter NEW because I made a
  mistake in the naming of the binary package, so I had to revise the package to
  make libnglib-6.2 (for the .1810 release) replace libnglib-6.2.1804.

* Feb 25: Sponsored `upload <https://ftp-master.debian.org/new/pycollada_0.6-1.html>`__
  of `pycollada <https://github.com/pycollada/pycollada>`_ which adds Python 3
  support and a python3- package, so it has to pass through NEW again.

* Feb 28: `Upload
  <https://tracker.debian.org/news/1033005/accepted-opencascade-730dfsg1-5-source-into-unstable/>`__
  of `OpenCASCADE <https://www.opencascade.com/>`_, revising the package to
  revert to the default 'opencascade' installation paths instead of 'occt' (a
  not-so-great packaging decision as OpenCASCADE was my 2nd ever Debian package)

Sponsorship
===========
Verbal support by way of my contact info below is greatly
appreciated, but if you want to help support my free software & open
engineering work financially, I've made it easy with several options:

* `Patreon <https://patreon.com/kkremitzki>`_
* `PayPal <https://paypal.me/kkremitzki>`_
* `Liberapay <https://liberapay.com/kkremitzki>`_
* `Wispay <https://www.wispay.io/t/0d7>`_ (cryptocurrency)

Any level of support is appreciated!

Contact
=======
You can follow me on Twitter `@thekurtwk <https://twitter.com/thekurtwk>`_.

I'm also now on `Matrix <https://matrix.org/blog/home/>`_, an open network for
secure, decentralized communication, `@kkremitzki:matrix.org
<https://matrix.to/#/@kkremitzki:matrix.org>`_.
