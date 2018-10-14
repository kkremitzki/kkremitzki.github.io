.. title: Free Software Activities in September 2018
.. slug: free-software-activities-in-september-2018
.. date: 2018-10-13 22:47:15 UTC-05:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text

Hello all, unfortunately my update comes late again this month, although I have good reason! I just finished landing a job
as a scientific software developer. From the looks of it, I'll mostly be working on things from a systems engineering perspective,
but it'll be in the context of the scientific Python ecosystem as well as involving Qt. This is nice in that while I will have less
free time to spend on FreeCAD, it will almost certainly be of increasingly higher quality.

Another interesting benefit of the job is that it will allow me to move back to Austin, which has the very well-equipped hackerspace
`ATX Hackerspace <http://atxhs.org>`_. I look forward to joining and having a chance to finally experiment with FreeCAD's CNC integrations,
and to have a great space to hack on hardware and software.

Now, finally, to summarize what I've worked on in the month of September.

- I created a `thread on the FreeCAD forums <https://forum.freecadweb.org/viewtopic.php?f=8&t=31046>`_ to announce the revival of the
  `FreeCAD Community Extras PPA <https://launchpad.net/~freecad-community/+archive/ubuntu/ppa>`_. This will be used to host packages of interest
  to the FreeCAD community, and things that need testing for possible future inclusion in FreeCAD. In retrospect, I should have used this PPA to get
  testers for the packages I was working on during my last Google Summer of Code.
- To this FreeCAD Community Extras PPA, I uploaded packages for:
    - `OpenCAMLIB <https://github.com/aewallin/opencamlib>`_, a C++ library with Python bindings for creating 3D toolpaths for CNC machines such as mills and lathes.
    - `OpenVoronoi <https://github.com/aewallin/openvoronoi>`_, another C++/Python library for 2D Voronoi diagrams for point and line-segment sites.
    - Laughlin Research's standalone `SMESH <https://github.com/LaughlinResearch/SMESH>`_, the Salome meshing framework.
    - `Netgen <https://github.com/NGSolve/netgen>`_'s latest release, 6.2.1807, a 3D tetrahedral mesh generator.
    - `IfcOpenShell <https://github.com/IfcOpenShell/IfcOpenShell>`_, an open source Python IFC library and geometry engine.
    - `IfcPlusPlus <https://github.com/ifcquery/ifcplusplus>`_, an open source C++ class model, reader, and writer for IFC files with simple Qt/OpenSceneGraph viewer application.
- I have long been interested in having CAD database support, and I spent quite a bit of September working with my friend on research and initial work for this. From what we've found,
  we can feasibly have a PostgreSQL extension similar to PostGIS, but for CAD: `PostCAD <https://github.com/postcad>`_. This would mainly involve a marriage between `OpenCASCADE <https://www.opencascade.com/>`_, the C++ geometry and topology kernel of FreeCAD,
  and `libpqxx <https://github.com/jtv/libpqxx>`_, the official C++ client library for PostgreSQL. The potential for such an extension would be huge, with all the power and features
  of PostgreSQL with an understanding of CAD data and geometry. For example, FreeCAD could interface with this database, and have the database take care of things like editing locks
  for models, permissions for readingn and writing of models, and so forth. Furthermore, by creating a database-level abstraction for CAD, that opens the way for web abstractions
  for CAD, similar to GeoDjango's GIS extensions for Django. That work could one day pave the way for a web interface for FreeCAD.

As always, if you appreciate the work I do with FreeCAD, the Debian Science Team, and Open Engineering on Linux, any level of support would be appreciated
`on my Patreon! <https://patreon.com/kkremitzki>`_
