.. title: Free Software Activities in August 2018
.. slug: free-software-activities-in-august-2018
.. date: 2018-09-12 05:20:13 UTC-05:00
.. tags: debian
.. category: 
.. link: 
.. description: 
.. type: text

Hello all! After reading some of the nice activity logs published by members of the
Debian Project at https://planet.debian.org, I've decided to publish my own version.
This will mostly be my work on FreeCAD and Debian, but will also include other points
of note from my many interests. I'll also include relevant activities for `my supporters
on Patreon <https://www.patreon.com/kkremitzki>`_

As covered in my previous post, most of the first half of August was spent finishing
my Google Summer of Code project for FreeCAD, which largely turned into "packaging
for the Debian Science Team" since FreeCAD's dependency chain and options for
integration are so vast. However, the nature of the work is highly parallel.
For example, when packaging, most issues occur either almost immediately into the build,
or after the build has finished. This means that after an initial bit of packaging work
that allows a build to actually proceed, one then has to launch the build and wait
anywhere from a few minutes to a few hours to see the next issue arise. So, as a
result, I worked on *many* packages in parallel. A negative consequence of this was
that I somewhat overloaded my plate in terms of things I can handle, so in actuality
this meant I would work on a handful of packages on several machines at once, and then
once those issues were largely resolved I would move onto another handful, rather
than really juggling them all at once.

After finishing GSoC, I first turned my attention to two of the packages I had
worked on in parallel, python-fluids and python-ulmo.

`python-fluids <https://tracker.debian.org/pkg/python-fluids>`_
###############################################################
I made a new upload for this package to correct several issues. Here's an excerpt from the changelog::

  * [1215102] Make python-fluids-doc Multi-Arch: foreign
  * [eb610fd] Correct Vcs-* fields
  * [62570cd] Updated to Standards-Version 4.2.0, no change required
  * [29e96a7] Correct debian/watch
  * [3e90d05] Add missing scipy dependency
  * [cd776a2] Add lintian override for
    package-contains-documentation-outside-usr-share-doc


The package still fails some reproducibility tests on i386 and could use a standards version bump, but other
than that, this package is almost completely clean now! It's quite satisfying cleaning up these packages.


`python-ulmo <https://tracker.debian.org/pkg/python-ulmo>`_
###########################################################
I made an upload for this package as well::

  * [7150daa] Correct Vcs-* fields
  * [027b50b] Mark python-ulmo-doc as Multi-Arch: foreign
  * [d72b6f6] Add patch to fix FutureWarning

The package was failing its autopkgtests because Python was emitting a FutureWarning onto stderr.
This package is actually fully reproducible, and only needs a standards version bump to be fully clean.

`gmsh <https://tracker.debian.org/pkg/gmsh>`_
#############################################
On August 22nd, `Gmsh 4.0.0 was released! <http://gmsh.info/>`_ The Java API was removed and a Julia one added.
This is a nice release because in 
`Debian bug #904946 <https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=904946>`_ it was found that the Gmsh package, after being updated to
be built against OCCT instead of OCE, actually no longer worked when used in FreeCAD, giving the error::

    Error   : Gmsh requires OpenCASCADE to import shape

My hope was that by updating to the new Gmsh version, this problem would resolve itself. However, I ran into a few problems and had to postpone
finishing up.

`netgen <https://tracker.debian.org/pkg/netgen>`_
#################################################
On August 19th, `Debian bug #906619 <https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=906619>`_ was reported against Netgen, which was
an occasion to look at the state of the package. I noticed that upstream had released version 6.2.1807 (versus the current .1804) but
it was not tagged in the Netgen repository, only as a submodule of the `Ngsolve repository <https://github.com/ngsolve/ngsolve>`_.

On August 31st, I packaged the new version and resolved the bug 
in `science-team/netgen PR #9 <https://salsa.debian.org/science-team/netgen/merge_requests/9/commits>`_.

salome-smesh
############
Although technically not August, on September 3rd I pushed the `nearly finished package for a standalone salome-smesh on Salsa <https://salsa.debian.org/kkremitzki-guest/salome-smesh>`_
which is fully functional except for an issue with the CMake config file. I submitted a pull request to support multi-arch for the package
but forgot to update the path in the CMake config file, so the variables therein have to be manually set, or the file edited.

cantera
#######
On August 24th, Cantera 2.4.0 was released::

    Cantera is an open-source suite of tools for problems involving chemical kinetics, thermodynamics, and transport processes.

Previously there had been an issue with the build, where the packages would be made successfully, but attempting to `import cantera` in
Python would error out, presumably due to the way an included copy of libfmt was handled during the build. However, the issue is no longer
present, so I now have a working Cantera 2.4.0 package! The only shortcoming is that I don't have working docs build yet, so this package
didn't make it in time for August.

`openfoam <https://tracker.debian.org/pkg/openfoam>`_
#####################################################
Previously I had submitted a pull request for OpenFOAM 6 to the Debian Science Team, but spontaneously the package began to fail,
presumably due to some change in a dependency. I spent some time troubleshooting this issue but haven't found a resolution yet.
Here's a snippet of the build failure::

        Allwmake src/Pstream
        wmake dummy
        wmakeLnIncludeAll: running wmakeLnInclude on dependent libraries:
            wmakeLnInclude: linking include files to /build/openfoam-6.20180805+dfsg1/src/OpenFOAM/lnInclude
            wmakeLnInclude: linking include files to /build/openfoam-6.20180805+dfsg1/src/OSspecific/POSIX/lnInclude
        make[2]: Entering directory '/build/openfoam-6.20180805+dfsg1/src/Pstream/dummy'
        wmakeLnInclude: linking include files to ./lnInclude
        make[2]: Leaving directory '/build/openfoam-6.20180805+dfsg1/src/Pstream/dummy'
        make[2]: Entering directory '/build/openfoam-6.20180805+dfsg1/src/Pstream/dummy'
        Making dependency list for source file UOPwrite.C
        realloc(): invalid next size
        make[2]: *** Deleting file '/build/openfoam-6.20180805+dfsg1/platforms/linux64GccDPInt32Opt/src/Pstream/dummy/UOPwrite.C.dep'
        Making dependency list for source file UIPread.C
        realloc(): invalid next size
        make[2]: *** Deleting file '/build/openfoam-6.20180805+dfsg1/platforms/linux64GccDPInt32Opt/src/Pstream/dummy/UIPread.C.dep'
        Making dependency list for source file UPstream.C
        realloc(): invalid next size
        make[2]: *** Deleting file '/build/openfoam-6.20180805+dfsg1/platforms/linux64GccDPInt32Opt/src/Pstream/dummy/UPstream.C.dep'


I'll have to continue investigating this one.

`pyside2 <https://tracker.debian.org/pkg/pyside2>`_
###################################################
I reported `Debian bug #906020 <https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=906020>`_ about missing Python 3 CMake config files,
which was fixed Aug 28th. I began investigating how this would Pivy builds, but got sidetracked by a problem with the `med-fichier` package.

`freecad <https://tracker.debian.org/pkg/freecad>`_
###################################################
I ran into some build issues trying to update the package now that my Debian Unstable workstation is running Qt 5.11::

    error: invalid use of incomplete type ‘class QAction’
         QAction* action = new QAction(tr("Remove"), this);

There are several instances of this throughout the codebase that can basically be fixed with by adding some `#include` s.

projectchrono
#############
There was a bit of discussion about utilization of `Project Chrono <http://www.projectchrono.org/>`_, an open source multi-physics simulation engine,
in FreeCAD. One problem with pursuing this is that it isn't packaged at all for Debian, which is rather surprising! It seems like high-quality software.
I began looking at packaging it and it actually doesn't seem that bad. One of the main issues is actually the naming: it's really long! There's also a
bit of worry about naming collisions I'll have to look into. As of now, I have a working package except for the Python bindings. Enabling them results
in this failure in the build process::

    [ 53%] Building CXX object src/demos/irrlicht/CMakeFiles/demo_IRR_soilbin.dir/demo_IRR_soilbin.cpp.o
    cd /build/project-chrono-3.0.0/obj-x86_64-linux-gnu/src/demos/irrlicht && /usr/lib/ccache/c++  -DBP_USE_FIXEDPOINT_INT_32 -I/build/project-chrono-3.0.0/src -I/build/project-chrono-3.0.0/obj-x86_64-linux-gnu -I/build/project-chrono-3.0.0/src/chrono -I/build/project-chrono-3.0.0/src/chrono/collision/bullet -I/build/project-chrono-3.0.0/src/chrono/collision/gimpact -I/build/project-chrono-3.0.0/src/chrono/collision/convexdecomposition/HACD -I/usr/include/irrlicht  -g -O2 -fdebug-prefix-map=/build/project-chrono-3.0.0=. -fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2 -pthread -fopenmp  -march=native -msse4.2 -mfpmath=sse  -march=native -mavx2  -march=native -mfma  -std=c++14 -pthread -fopenmp  -march=native -msse4.2 -mfpmath=sse  -march=native -mavx2  -march=native -mfma    -std=c++14 -pthread -fopenmp  -march=native -msse4.2 -mfpmath=sse  -march=native -mavx2  -march=native -mfma  -o CMakeFiles/demo_IRR_soilbin.dir/demo_IRR_soilbin.cpp.o -c /build/project-chrono-3.0.0/src/demos/irrlicht/demo_IRR_soilbin.cpp
    /build/project-chrono-3.0.0/obj-x86_64-linux-gnu/swig/ChModuleCorePYTHON_wrap.cxx: In member function 'virtual void chrono::ChLogPython::Output(const char*, size_t)':
    /build/project-chrono-3.0.0/obj-x86_64-linux-gnu/swig/ChModuleCorePYTHON_wrap.cxx:7610:23: error: format not a string literal and no format arguments [-Werror=format-security]
         PySys_WriteStdout(buffer);
                           ^~~~~~

opencamlib
##########
There was a problem with this package's doc depends, which I fixed at the end of August. However, it's still awaiting sponsorship to be uploaded
into the Debian archives.

med-fichier
###########
The `med-fichier package <https://tracker.debian.org/pkg/med-fichier>`_ in Debian currently is built with autotools but somewhat supports CMake builds, which
would be nice to switch to as it would provide CMake configuration files in libmedc-dev. I worked on updating the package, but currently building docs is broken,
and for some reason, the Fortran library is being statically linked.

Planet FreeCAD
##############
The `planet-venus package <https://tracker.debian.org/pkg/planet-venus>`_ in Debian is available for running your own RSS feed aggregation service.
I wanted to set up a planet.freecad.io to provide exactly that. However, the current version of the package is broken, and it only works in Debian 7, a.k.a. old-old-stable.

I spent some time researching the state of the package, but it's fairly rough, and most importantly, upstream is far from active. I'd like to run the RSS service but
fixing the package seems like a tall order.

freecad.io
##########
We previously had two servers available to run some of the web services for the FreeCAD project, but sadly they rebooted but never came back online.

I'm now paying for a VPS in Frankfurt using the money from `my Patreon <https://patreon.com/kkremitzki>`_. Unfortunately, it's a bit resource-strained
from the FreeIPA server hogging things. 

If you like my work as described above and would like to support me continuing to improve the state of open engineering on Linux, `please contribute to my Patreon! <https://patreon.com/kkremitzki>`_
######################################################################################################################################################################################################
