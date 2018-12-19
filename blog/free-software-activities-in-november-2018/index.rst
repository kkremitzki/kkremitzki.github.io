.. title: Free Software Activities in November 2018
.. slug: free-software-activities-in-november-2018
.. date: 2018-12-18 23:20:10 UTC-06:00
.. tags: debian,freecad,postcad
.. category: 
.. link: 
.. description: 
.. type: text

Intro
=====

Welcome to another of my monthly summaries on my work in the free software
world. My mission is to make engineering and science available for everyone,
and Debian, the Universal Operating System, is my weapon of choice.

I received some feedback on my last post that I made it seem I would be
stepping away from my role maintaining FreeCAD and other packages on the Debian
Science Team, which was an unfortunate miscommunication on my part. Mainly, I
just would like to reduce the proportion of my overall free software time on
it, from its current amount, nearly 100%, to a roughly even 1/3rd split between
Debian Science, FreeCAD, and PostCAD. The latter is a promising personal
project to make an OpenCASCADE-powered CAD extension for PostgreSQL, bringing
support for CAD file formats, datatypes, and algorithms to the powerful
Postgres ecosystem, similar to what PostCAD has done for geospatial analysis.
This could serve as a backend for both FreeCAD in the short term, and in the
long term, it could power a web-based version of FreeCAD, perhaps with some
Django-powered middleware serving a REST API for some WebGL-based frontend.

So, besides summarizing my work this month, I also plan to give a synopsis on
my Debian packaging, for both what's in-progress and on my wishlist. As you'll
see, it's quite extensive. My hope is that by whittling away at both lists, my
Debian Science work can focus more on maintenance of existing packages, and
free up some time for other things.

Sponsors
========
My work on Debian Science, FreeCAD, and PostCAD is `supported by my patrons on
Patreon <https://patreon.com/kkremitzki>`. While I had created a Liberapay a
while back, I never got any traction with it, and I found out recently that it
was because I had not set it up to actually receive payments. So, if you don't
like Patreon for whatever reason, you can also `support me on Liberapay
<https://liberapay.com/kkremitzki>`_. Just to round things out, if you don't
like either of those platforms, you can also `help support my work via PayPal
<https://paypal.me/kkremitzki>`_.

Transition for coin3
====================
Coin3D is a scene graph library and a fundamental part of FreeCAD.
Unfortunately, it hasn't had a release since 2011, but development has been
picking up recently, so it's likely that a release is not too far off. Even
without a formal release, several improvements have been made including CMake
support, so it's time to prepare a transition in advance of the Debian 10
release. Luckily, Leo Palomo-Avellaneda has taken the initiative of getting
this transition started.

Currently, the new Coin3D package is available in Debian Experimental as we
prepare the reverse-dependencies to build against it. For FreeCAD, we directly
depend on Pivy, which are Python bindings for Coin. Pivy, in turn, depends on
Coin and SoQt, which is a Qt GUI component toolkit library for Coin. A
pre-release version of SoQt is also being packaged since, like Coin, CMake
support has been added, as well as support for Qt 5.

Unfortunately, I've been grinding my gears on building Pivy against the new
Coin and SoQt for a good part of this month, which is especially troublesome
since FreeCAD's transition to Python 3 is blocked by the upload of a new Pivy,
which I prepared earlier this year.

With any luck, I'll be able to help Leo finish the Coin and SoQt transition and
have Pivy prepared in December.

Gmsh Update
===========
Gmsh is a 3D finite element mesh generator with built-in pre- and
post-processing facilities. It's also one of the main meshers used by FreeCAD's
Finite Element Modeling Workbench, besides Netgen.

Currently Debian has Gmsh 3.0.6, but a new major version was released in
August. I've already prepared this new major version for testing in FreeCAD's
Community Extras PPA, but I hadn't cleaned up the packaging yet to submit to
Debian. However, in November, there were two point releases, 4.0.5 and 4.0.6,
so I wasn't able to complete this work this month, but I'm sure it'll be done
in early December.

One major piece of information regarding Gmsh 4 is a change in the API: the
libjava-gmsh3 package in Debian was never meant to be a public API, and so Gmsh
upstream has requested that we no longer ship it. To offset this, there have
been refinements for the actual public API, which officially comes in C, Python
3 and (new) Julia flavors. However, I haven't found much information on Julia
packaging in Debian, so I'll likely hold off on that package.

PySide 2 Rebuild & PPA Plans
============================
Since FreeCAD is an LGPL-licensed Qt project, we must use PySide and not PyQt
to do Qt things with Python. Because of this, the FreeCAD migration to Qt 5 on
Debian was blocked by the packaging of PySide 2, which was completed by
Freexian SARL over the summer. In Debian, we now have a Qt 5-enabled FreeCAD,
although our daily builds PPA is still using Qt 4.

Besides the Qt 4->5 transition, we're also finishing up a Python 2->3
transition. At the end of the summer I published a `freecad-python3` package in
the PPA which also used Qt 5. However, it wasn't really fully usable, moreso a
proof-of-concept that such a build indeed buildable.

At this point, the Debian FreeCAD package has begun to diverge from the FreeCAD
PPAs; besides Qt 5 builds not being available currently, the Debian package has
also been split into several packages (e.g. `libfreecad`, `freecad-common`,
etc. packages) in order to better comply with Debian Policy and the Filesystem
Hierarchy Standard.

So, there's a bit of work to do to catch the PPAs up. First, the package split
needs to be done. Then, I need to upload an alternative `freecad-daily` package
for Qt 5 builds, separate from Python 3. Once that is done and has undergone
some testing, `freecad-daily` can be replaced by it, and it in turn can be
replaced by a `freecad-python3` package for further testing. Since FreeCAD's
0.18 release is imminent, I'll need to get this taken care of during December,
so stay tuned.

Packaging in Progress
=====================
My first packaging list is all the software I've already started packaging. For
some, it's almost complete, and for others, I've only just begun. 

The purpose of these lists is not to give status updates, but to announce what
all I'm interested in to anyone reading this, and to give an idea of how much
packaging work I have in mind to improve this usage of Debian.

cantera
-------
`Homepage <https://cantera.org/>`__, `GitHub <https://github.com/Cantera/cantera>`__
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
    Cantera is an open-source suite of tools for problems involving chemical
    kinetics, thermodynamics, and transport processes.

I had this package working and waiting to be sponsored, but it looks like it currently fails
to build from source, so this just requires some maintenance.

coolprop
--------
`Homepage <http://www.coolprop.org/>`__, `GitHub <https://github.com/CoolProp/CoolProp>`__
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
    CoolProp is a thermophysical property database and wrappers for a selection
    of programming environments. It offers similar functionality to REFPROP,
    although CoolProp is open-source and free.

This package was previously building completely, but failing when one would attempt to do
an `import coolprop`. Now that it's been a while since I worked with it, it
seems to be failing to build.

elmerfem
--------
`Homepage <http://www.elmerfem.org/>`__, `GitHub <https://github.com/ElmerCSC/elmerfem>`__
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
    Elmer is a finite element software for numerical solution of partial
    differential equations. Elmer is capable of handling any number of equations
    and is therefore ideally suited for the simulation of multiphysical problems.
    It includes models, for example, of structural mechanics, fluid dynamics, heat
    transfer and electromagnetics. Users can also write their own equations that
    can be dynamically linked with the main program.

This was previously in Debian but removed due to abandonment, so a great deal
of the work is already done, but it also requires quite a bit of updating to
current Debian standards.

if97
----
`PDF Standard <http://www.iapws.org/relguide/IF97-Rev.pdf>`__, `GitHub <https://github.com/CoolProp/IF97>`__
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

    Open-source C++ implementation of the IAPWS-IF97 equations to calculate
    properties of the pure water substance.

This is a dependency of CoolProp, and I already have it packaged and waiting
for sponsorship at https://salsa.debian.org/science-team/if97.

ifcopenshell
------------
`Homepage <http://www.ifcopenshell.org/>`__, `GitHub <https://github.com/IfcOpenShell/IfcOpenShell>`__
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
    IfcOpenShell is an open source (LGPL) software library that helps users and
    software developers to work with the IFC file format. The IFC file format
    can be used to describe building and construction data. The format is
    commonly used for Building Information Modelling. IfcOpenShell uses
    OpenCASCADE internally to convert the implicit geometry in IFC files into
    explicit geometry that any software CAD or modelling package can
    understand.

I already have this packaged and awaiting sponsorship at https://salsa.debian.org/kkremitzki-guest/ifcopenshell.

It's also available on the `FreeCAD Community Extras PPA <https://launchpad.net/~freecad-community/+archive/ubuntu/ppa>`_.

ifcplusplus
-----------
`Homepage <http://ifcquery.com/>`__, `GitHub <https://github.com/ifcquery/ifcplusplus>`__
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
    IfcPlusPlus is an open source C++ class model, as well as a reader and
    writer for IFC files in STEP format. It features easy and efficient memory
    management using smart pointers, a parallel reader for fast parsing on
    multi-core CPU's, and a simple IFC viewer application using Qt and
    OpenSceneGraph.

I already have this packaged and awaiting sponsorship at https://salsa.debian.org/kkremitzki-guest/ifcplusplus.

It's also available on the `FreeCAD Community Extras PPA <https://launchpad.net/~freecad-community/+archive/ubuntu/ppa>`_.

opencamlib
----------
`Homepage <http://www.anderswallin.net/tag/opencamlib/>`__, `GitHub <https://github.com/aewallin/opencamlib>`__
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
    OpenCAMLib (OCL) is a C++ library with Python bindings for creating 3D
    toolpaths for CNC-machines such as mills and lathes. 

I already have this packaged and awaiting sponsorship at https://salsa.debian.org/science-team/opencamlib.

It's also available on the `FreeCAD Community Extras PPA <https://launchpad.net/~freecad-community/+archive/ubuntu/ppa>`_.

openvoronoi
-----------
`Homepage <http://www.anderswallin.net/category/cnc/cam/openvoronoi/>`__, `GitHub <https://github.com/aewallin/openvoronoi>`__
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
    2D voronoi diagram for point and line-segment sites using incremental
    topology-oriented algorithm. C++ with Python bindings.

I already have this packaged and awaiting sponsorship at https://salsa.debian.org/kkremitzki-guest/openvoronoi.

It's also available on the `FreeCAD Community Extras PPA <https://launchpad.net/~freecad-community/+archive/ubuntu/ppa>`_.

projectchrono
-------------
`Homepage <https://projectchrono.org/>`__, `GitHub <https://github.com/projectchrono/chrono>`__
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
    C++ library for multi-physics simulation. The applications areas in which
    Chrono is most often used are vehicle dynamics, robotics, and machine
    design. In vehicle dynamics, Chrono has mature support for tire/terrain
    interaction modeling and simulation.


I've only roughly begun packaging this, and I'm already tired of typing
`libprojectchrono`. Anyway, it's a rather large set of components which will be
broken up into several packages. Luckily, things are done in a pretty normal
way so I don't imagine this will be difficult to finish packaging, just a
little time-costly.

smesh
-----
`GitHub <https://github.com/LaughlinResearch/smesh>`__
""""""""""""""""""""""""""""""""""""""""""""""""""""""
    A stand-alone library of the mesh framework from the Salome Platform

I've gotten this standalone version of SMESH packaged and awaiting sponsorship
at https://salsa.debian.org/kkremitzki-guest/salome-smesh.  Eventually, I want
to package the entire Salome Platform, but it's extremely large and really
several source packages. Packaging this as an intermediate step allows us to
remove SMESH from FreeCAD's included sources.

It's also available on the `FreeCAD Community Extras PPA
<https://launchpad.net/~freecad-community/+archive/ubuntu/ppa>`_.

xcfem
-----
`Homepage <https://sites.google.com/site/xcfemanalysis/>`__, `GitHub <https://github.com/xcfem/xc>`__
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
    XC is an open source FEA program designed to solve structural analysis
    problems.

This library is supposed to be an alternative to the not-quite-freely licensed
OpenSees, which is used in seismic research and analysis. There has been some
interest in the FreeCAD forums about using this, so I'm beginning packaging it
in advance. However, it seems a bit complicated as it requires multiple
sources, the GitHub `xcfem/xc` repo as well as `xcfem/xc_utils`.

Wishlist Packages
=================

2geom
-----
`Homepage <http://lib2geom.sourceforge.net/>`__, `GitLab <https://gitlab.com/inkscape/lib2geom>`__
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
    lib2geom (2Geom in private life) was initially a library developed for
    Inkscape but will provide a robust computational geometry framework for any
    application. It is not a rendering library, instead concentrating on high
    level algorithms such as computing arc length.

I looked at this package and it seemed like it will be straightforward to
package, and with the parent project's popularity, someone else may get to it
first.

bimserver
---------
`Homepage <bimserver.org>`__, `GitHub <https://github.com/opensourceBIM/BIMserver>`__
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
    The Building Information Model server (short: BIMserver) enables you to
    store and manage the information of a construction (or other building
    related) project. Data is stored in the open standard IFC. The BIMserver is
    not a fileserver, but it uses a model-driven architecture approach. This
    means that IFC data is stored in an underlying database. The main advantage
    of this approach is the ability to query, merge and filter the BIM-model
    and generate IFC files on the fly.

The integration of BIM with FreeCAD is a very promising endeavor, and letting
FreeCAD be the client in a client-server model provides many potential
benefits. (This is the reason I'm working on PostCAD.) Packaging BIMserver 
is a natural decision, then. However, it's a Java application, which I have
little experience with language-wise and none in terms of packaging it in
Debian, so this one has a bit of a difficulty associated with it.

cadquery
--------
`Homepage <https://dcowden.github.io/cadquery/index.html>`__, `GitHub <https://github.com/dcowden/cadquery>`__
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
    CadQuery is an intuitive, easy-to-use python based language for building
    parametric 3D CAD models. CadQuery is for 3D CAD what jQuery is for
    javascript. Imagine selecting Faces of a 3d object the same way you select
    DOM objects with JQuery!

CadQuery is an interesting project which actually makes use of FreeCAD, and
indeed FreeCAD even has a CadQuery Workbench. This would be nice to package as
a way of extending the FreeCAD ecosystem on Debian.

Unfortunately, CadQuery 2 is planning on moving away from FreeCAD to PythonOCC,
which is based on the now behind-the-times OpenCASCADE Community Edition fork,
based on OpenCASCADE 6.9.1; FreeCAD and other projects are moving back to the
mainline OpenCASCADE Technology project which is about to release version
7.4.0. It would be nice if both CadQuery and FreeCAD could instead move to use
PyOCCT as a middle-layer between itself and OpenCASCADE.

libreoffice-code-highlighter 
----------------------------
`Homepage <https://extensions.libreoffice.org/extensions/code-highlighter>`__, `GitHub <https://github.com/slgobinath/libreoffice-code-highlighter>`__
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
    This extension highlights the code snippets for over 350 languages in
    LibreOffice.

I have packaged a LibreOffice extension before, and it was fairly easy, so I expect this one will be too. However its priority is rather low.

lib3mf
------
`Homepage <https://3mf.io/>`__, `GitHub <https://github.com/3MFConsortium/lib3mf>`__
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
    Lib3MF is a C++ implementation of the 3D Manufacturing Format file standard.

This seems like a straightforward library to package, but there is no pressing need as FreeCAD does not support it yet.

muesli
------
`Homepage <https://materials.imdea.org/research/simulation-tools/muesli/>`__, `BitBucket <https://bitbucket.org/ignromero/muesli>`__
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
    MUESLI, a Material UnivErSal LIbrary, is a collection of C++ classes and
    functions designed to model material behavior at the continuum level.
    Developed at IMDEA Materials, it is available to the material science and
    computational mechanics community as a suite of standard models and as a
    platform for developing new ones.

This seems like a great candidate package for Debian Science but I have had
some difficulty building it, which I need to conquer before packaging can
begin.

cling
-----
`Homepage <https://root.cern.ch/cling>`__, `GitHub <https://github.com/root-project/cling>`__
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
    Cling is an interactive C++ interpreter, built on top of Clang and LLVM
    compiler infrastructure. Cling realizes the read-eval-print loop (REPL)
    concept, in order to leverage rapid application development. Implemented as
    a small extension to LLVM and Clang, the interpreter reuses their strengths
    such as the praised concise and expressive compiler diagnostics.

cling is an incredible project which should have been packaged already.
Hopefully someone else gets to it first.

dpkg-licenses
-------------
`GitHub <https://github.com/daald/dpkg-licenses>`__
"""""""""""""""""""""""""""""""""""""""""""""""""""
    A command line tool which lists the licenses of all installed packages in a Debian-based system (like Ubuntu)

This is a small script which gives a summary of the licenses used by the installed packages on your system--a good way to audit packages, e.g. forbidding AGPL.

landlab
-------
`Homepage <https://landlab.github.io/#/#install>`__, `GitHub <https://github.com/landlab/landlab>`__
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
     Landlab is a Python-based modeling environment that allows scientists and
     students to build numerical landscape models. Designed for disciplines
     that quantify earth surface dynamics such as geomorphology, hydrology,
     glaciology, and stratigraphy, it can also be used in related fields.

     Landlab provides components to compute flows (such as water, sediment,
     glacial ice, volcanic material, or landslide debris) across a gridded
     terrain. With its robust, reusable components, Landlab allows scientists
     to quickly build landscape model experiments and compute mass balance
     across scales. 

Landlab is another interesting Debian Science candidate but I have no pressing need to package it.

nikola
------
`Homepage <https://getnikola.com/>`__, `GitHub <https://github.com/getnikola/nikola>`__
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
    A static website and blog generator, written in Python.

Nikola is what I use to create this blog, but it's somewhat fast moving and a
slow maintainer in Debian previously caused problems, so I don't want to pick
this up until I've leveled up my package maintenance.

osifont
-------
`Homepage <https://fontlibrary.org/en/font/osifont>`__, `GitHub <https://github.com/hikikomori82/osifont>`__
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
    In some European countries, CAD projects must have font which conform to
    IS0 3O98 specification. Commercial CADs has this font, but free CADs not.
    There is no available free font yet, so this project will fix this. This
    font will be created completely from the scratch. Font is created with free
    tools like FontForge, Inkscape, Gimp. Font is available under 3 licences:
    GNU GPL licence version 3 with GPL font exception, GNU GPL licence version
    2 with GPL font exception, GNU LGPL licence version 3 with GPL font
    exception.

This is a bundled font with FreeCAD, so I'd like to separate into its own
package. However, the need to package it is not pressing, so I haven't picked
it up.

pigpio
------
`Homepage <http://abyz.me.uk/rpi/pigpio/>`__, `GitHub <https://github.com/joan2937/pigpio>`__
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
    pigpio is a C library for the Raspberry which allows control of the General
    Purpose Input Outputs (GPIO).

This is an important tool for teaching with Raspberry Pi's and should be
packaged as soon as possible, I've just had more pressing concerns.

piscope
-------
`Homepage <http://abyz.me.uk/rpi/pigpio/piscope.html>`__, `GitHub <https://github.com/joan2937/piscope>`__
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
    A logic analyser (digital waveform viewer).  piscope uses the services of
    the pigpio library. pigpio needs to be running on the Pi whose gpios are to
    be monitored.

Being able to see the waveform of a GPIO pin on a Raspberry Pi is incredibly
useful for teaching robotics and electrical engineering classes with them. This
also needs to be packaged.

pyocct
------
`GitHub <https://github.com/LaughlinResearch/pyOCCT>`__
"""""""""""""""""""""""""""""""""""""""""""""""""""""""
    The pyOCCT project provides Python bindings to the OpenCASCADE 7.2.0
    geometry kernel and SMESH 8.3.0 meshing library via pybind11. Together,
    this technology stack enables rapid CAD/CAE application development in the
    popular Python programming language.

This is a very promising library for Python OpenCASCADE development, so I'd
like to get it packaged, but it's blocked by getting SMESH packaged.

pyray
-----
`GitHub <https://github.com/ryu577/pyray>`__
""""""""""""""""""""""""""""""""""""""""""""
    A 3D rendering library written completely in Python. 

A promising library for integrating raytracing functionality directly into
FreeCAD, and for general raytracing in Python.

quarter
-------
`BitBucket <https://bitbucket.org/Coin3D/quarter>`__
""""""""""""""""""""""""""""""""""""""""""""""""""""
    Quarter is a light-weight glue library that provides seamless integration
    between the Coin high-level 3D visualization library and Qt's 2D user
    interface library.  The functionality in Quarter revolves around
    QuarterWidget, a subclass of QGLWidget. This widget provides functionality
    for rendering of Coin scenegraphs and translation of QEvents into SoEvents.
    Using this widget is as easy as using any other QWidget.

FreeCAD already uses an included (and slightly modified) copy of Quarter in its
source, so I'd like to package Quarter in a standalone fashion as part of
moving FreeCAD away from bundled copies in its source.

rebound
-------
`Homepage <https://rebound.readthedocs.io/en/latest/>`__, `GitHub <https://github.com/hannorein/rebound>`__
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
    REBOUND is an N-body integrator, i.e. a software package that can integrate
    the motion of particles under the influence of gravity. The particles can
    represent stars, planets, moons, ring or dust particles. REBOUND is very
    flexible and can be customized to accurately and efficiently solve many
    problems in astrophysics.

This seems like a really great library to have in Debian Science, but it's not a priority.

sqlint      
------
`GitHub <https://github.com/purcell/sqlint>`__
""""""""""""""""""""""""""""""""""""""""""""""
    SQLint is a simple command-line linter which reads your SQL files and
    reports any syntax errors or warnings it finds.

    At this stage, SQLint checks SQL against the ANSI syntax, and uses the
    PostgreSQL SQL parser to achieve this. In time, we hope to add support for
    non-standard SQL variants (e.g. MySQL). Contributions are welcome.

This would be a very useful utility to have in Debian, but I always write SQL without flaw the first try. (wink)

swatmodel
---------
`Homepage <https://swat.tamu.edu/>`__, `GitHub <https://github.com/WatershedModels/SWAT>`__
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
    The Soil & Water Assessment Tool is a small watershed to river basin-scale
    model used to simulate the quality and quantity of surface and ground water
    and predict the environmental impact of land use, land management
    practices, and climate change. SWAT is widely used in assessing soil
    erosion prevention and control, non-point source pollution control and
    regional management in watersheds.

SWAT is a powerful research tool in agricultural engineering, among several
others I'm interested in eventually packaging for Debian. The planned package
will be based on a CMake-enabled fork of the upstream source, which is built
with Intel's Fortran compiler by default and also had to be adapted for
gfortran.

wger
----
`Homepage <https://wger.de/en/software/features>`__, `GitHub <https://github.com/wger-project/wger>`__
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
    Self hosted FLOSS fitness/workout and weight tracker written with Django

This is a very promising application which could be used as both a fitness
tracker as well as a weight/nutrition tracker, something along the lines of a
self-hosted MyFitnessPal. However, my other packaging priorities outweigh this
at the moment.

Conclusion
==========
So, there you have it! My mostly complete list of in-progress and wishlist
items for Debian packaging. If you have any feedback on packages on the list,
or want to get in touch with me, you can find me `on Twitter
<https://twitter.com/thekurtwk>`_ or send me an email at kurt at kwk.systems.
I'll also be starting to stream my Debian & FreeCAD work very soon, `subscribe
to me on Twitch <https://twitch.tv/kkremitzki>`_ to get notified when I go
live.
