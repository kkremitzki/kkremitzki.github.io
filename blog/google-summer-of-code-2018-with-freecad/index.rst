.. title: Google Summer of Code 2018 with FreeCAD
.. slug: google-summer-of-code-2018-with-freecad
.. date: 2018-08-14 03:51:37 UTC-05:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text

Hello all! This post is my final work product for GSoC 2018 for the FreeCAD project.
The main center for communication for FreeCAD is the forums, but we also coordinated things
through the #freecad channel on Freenode.
`The main thread for my project was here. <https://forum.freecadweb.org/viewtopic.php?f=8&t=28478>`_

To summarize my project: FreeCAD is a complex application with an extensive dependency tree. The packaging
situation has always trailed the tip of development, which means users don't get to see the best FreeCAD
has to offer, and people trying to help new users have to deal with sometimes years-old bugs.
The goal was to improve the general ecosystem of the FreeCAD stack, and to cut down on technical debt to
make things easier moving forward. After some consideration it was decided to focus on Debian packaging
since that would be the most 'ecologically good'.

I began with a rough knowledge of Debian packaging, but now feel competent
enough to want to take over the maintenance of Debian packaging for FreeCAD and several other packages
within the Debian Science Team, which will improve the free software engineering experience in Debian 
as well as its derivatives such as Ubuntu and Linux Mint.

This post will summarize my work throughout the summer chronologically, mostly linking to emails in
the Debian Science mailing list, pull requests on Debian's Gitlab instance or Github, and to some repositories.

More detailed information can be found at https://salsa.debian.org/users/kkremitzki-guest.

Coding Period 0, Community Bonding Period (April 23 - May 14)
#############################################################
* May 8: RFS for python-fluids: https://lists.debian.org/debian-science/2018/05/msg00044.html
	* Packaging this was part of learning more about Debian packaging, and because I'm a fan of the library
	  for its use in fluids engineering - part of overall ecosystem improvements.

Coding Period 1 (May 14 - June 15)
##################################
* Most of the first coding period was spent working on FreeCAD 0.17 packaging, as well as packaging Netgen 6.2.1804
  and updating Gmsh to use OCCT, which I packaged prior to GSoC. I didn't finish them quite in time for submission
  within the first coding period. I also spent time working on packaging PySide 2, which is a dependency for
  FreeCAD's transition to Qt 5 & Python 3, but backed away after finding it was being worked on by others.


* May 17: Netgen PR (Remove unnecessary backup files): https://github.com/NGSolve/netgen/pull/15
	* Preparation work for packaging Netgen, which is used as a mesher by FreeCAD.
* May 25: Discussion of Netgen 6.2.1804 work: https://lists.debian.org/debian-science/2018/05/msg00101.html
        * This was just me announcing that I was working on this so as to help not duplicate work.

Coding Period 2 (June 15 - July 13)
###################################
* June 19: Improvements to fluids after suggestions: https://lists.debian.org/debian-science/2018/06/msg00031.html
* June 20: OpenFOAM 5 experimentation announced: https://lists.debian.org/debian-science/2018/06/msg00038.html
	* This package is part of the FreeCAD ecosystem by way of its CFD (Computational Fluid Dynamics) workbench.
* June 21: RFS for netgen: https://lists.debian.org/debian-science/2018/06/msg00039.html
	* Note: RFS = request for sponsorship, i.e. a submission of packaging work for Debian project members.
* June 21: RFS for gmsh: https://lists.debian.org/debian-science/2018/06/msg00040.html
	* Gmsh is another mesher used by FreeCAD.
* June 21: RFS for freecad: https://lists.debian.org/debian-science/2018/06/msg00041.html
	* This was the packaging work for the FreeCAD 0.17 release.
* June 21: RFS for if97: https://lists.debian.org/debian-science/2018/06/msg00042.html
	* This was another ecosystem project I worked on, a dependency for CoolProp, a powerful thermodynamics library.
* July 8: FreeCAD PR (Detect OCCT at new Debian location): https://github.com/FreeCAD/FreeCAD/pull/1545
	* This was a housekeeping PR as a result of my Debian packaging work.
* July 8: FreeCAD-Doc initial commit: https://github.com/FreeCAD/FreeCAD-Doc/commits/master
	* The freecad-doc package was removed from Debian in 2016 for Debian Free Software Guidelines reasons.
* July 11: Updated PPA to OCCT 7.3: https://launchpad.net/~freecad-maintainers/+archive/ubuntu/freecad-daily/+packages
	* This was a backport of Debian packaging work for OCCT 7.3

Coding Period 3 (July 13 - Aug 14)
##################################
* July 26: PR for horizon-eda (Support build against OCCT): https://github.com/carrotIndustries/horizon/pull/181/files
	* As part of packaging OCCT, it is planned to phase out OCE (a community fork of OCCT which has stalled in development) and this
	  was more housekeeping work.
* July 27: PR for deal.ii (Update dependencies & rules for liboce->libocct transition): https://salsa.debian.org/science-team/deal.ii/merge_requests/1
	* Similar as above.
* July 29: RFS for ulmo: https://lists.debian.org/debian-science/2018/07/msg00042.html
	* This was an ecosystem packaging work, as this library was very useful for me in hydrology and for various agricultural engineering data needs.
* Aug 7: RFS for openfoam: https://lists.debian.org/debian-science/2018/08/msg00011.html
	* My submission for OpenFOAM 5 was delayed by the release of OpenFOAM 6.
* Aug 8: RFS for openvoronoi: https://lists.debian.org/debian-science/2018/08/msg00022.html
	* This was a new dependency for FreeCAD's Path workbench which was relicensed so it could be directly integrated.
* Aug 8: RFS for opencamlib: https://lists.debian.org/debian-science/2018/08/msg00023.html
	* Similar as above.
* Aug 10: PR for smesh (Fix GCC8 FTBFS): https://github.com/LaughlinResearch/SMESH/pull/9
	* Part of packaging work for SMESH, a mesher used by FreeCAD which is included in the FreeCAD source (which is generally undesirable, and so packaging it would allow us to remove the included copy.)
* Aug 12: RFS for pivy: https://lists.debian.org/debian-science/2018/08/msg00041.html
	* PySide 2 was a dependency for pivy, so once it was packaged I was able to submit my work for pivy, which required upstreaming Python 3 support from FreeCAD's fork. This package was the last dependency for FreeCAD's Qt 5 & Python 3 transition. 
* Aug 14: RFS for freecad-doc: https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=906105
	* Packaging for freecad-doc was delayed by my desire, by way of providing a multi-language supported package, to say thanks to the FreeCAD community translators who provided thorough French and Italian translations.
* Aug 14: SMESH repo: https://salsa.debian.org/kkremitzki-guest/salome-smesh
	* Packaging external SMESH is incomplete, as its current CMake instructions don't append the library version to the shared library, which will require patching.
* Aug 14: CoolProp repo: https://salsa.debian.org/kkremitzki-guest/coolprop
	* Similar as above.

Now that GSoC is done I am excited to continue working within the Debian Science Team. Besides an upcoming FreeCAD 0.18 release,
I have several packages I plan to make improvements to and to package for Debian, and ultimately to integrate into future
FreeCAD workbenches as part of my plan to make it the ultimate 3D engineering toolbox!

Therefore, I must say thanks to the FreeCAD and Debian communities for working with me, and to my GSoC mentors and GSoC itself
for providing me this wonderful opportunity. May it continue providing valuable opportunities for others for many years to come.
