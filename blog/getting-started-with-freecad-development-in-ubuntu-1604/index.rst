.. title: Getting Started with FreeCAD Development in Ubuntu 16.04
.. slug: getting-started-with-freecad-development-in-ubuntu-1604
.. date: 2016-06-05 06:17:51 UTC-05:00
.. tags: foss,freecad,linux
.. category: 
.. link: 
.. description: 
.. type: text


`FreeCAD
<http://www.freecadweb.org/>`_ is a multi-platform (Windows, Mac, Linux) open source parametric 3D CAD modeler, and can read
and write many open file formats. 

An explanation of the many virtues of open source software can be found at `Open Source for America
<http://opensourceforamerica.org/learn-more/benefits-of-open-source-software/>`_ and elsewhere. To quote OSFA,

  The Open Source model harnesses the power of distributed peer review and transparency to create high-quality, secure 
  and easily integrated software at an accelerated pace and lower cost.

Commerical-grade CAD software, while incredibly useful, has several downsides including being locked behind 4 or 5 digit licensing costs,
and its use in amateur projects or the developing world is often facilitated by piracy. FreeCAD, on the other hand, is free as in beer 
and free as in freedom, although it is currently under development. However, one of the benefits of the open source model is the ease
with which interested people can contribute to the project and make better tools for all mankind.

While using FreeCAD, I noticed a few typos in the menus; although my first contribution to the project wasn't too significant, I
documented the process of getting a development environment set up on my Ubuntu 16.04 desktop so that others could follow the same
steps and begin contributing.


1. Pull down a copy of the code. (If you don't have a copy of git, run ``sudo apt-get install git``.)

  .. code-block:: bash

    git clone https://github.com/FreeCAD/FreeCAD.git freecad-code
    mkdir freecad-build

2. Install all dependencies.

  .. code-block:: bash

    sudo apt-get install build-essential cmake python python-matplotlib libtool libcoin80-dev \
      libsoqt4-dev libxerces-c-dev libboost-dev libboost-filesystem-dev libboost-regex-dev  \
      libboost-program-options-dev libboost-signals-dev libboost-thread-dev libboost-python-dev \
      libqt4-dev libqt4-opengl-dev qt4-dev-tools python-dev python-pyside pyside-tools 'liboce*-dev' \
      oce-draw libeigen3-dev libqtwebkit-dev libshiboken-dev libpyside-dev libode-dev swig libzipios++-dev \
      libfreetype6 libfreetype6-dev 

    # Install optional packages
    sudo apt-get install libsimage-dev checkinstall python-pivy python-qt4 doxygen \
      libcoin80-doc libspnav-dev

3. Move into build folder, make and compile the software. Use the ``-j $(nproc)`` flag to use all N of your CPU cores
   when compiling; some recommend using N + 1 CPU cores, which can be done by instead running ``make -j$(( $(nproc) + 1 )) .``.
   Don't forget the period at the end of the ``make`` command, which tells it to put the compiled software in the current
   ``freecad-build`` directory; it's good to keep the source code and build directories separate.

  .. code-block:: bash

    cd freecad-build
    cmake ../freecad-code
    make -j$(nproc) .

4. Fix Ubuntu 64-bit issue. If you are using a 64-bit version of Ubuntu (hopefully), you may run in to the following
   error message, which occurs because the expected ``libfreeimage.so`` file was moved into a subdirectory of ``/usr/lib/``.

  .. code-block:: bash

    make[2]: *** No rule to make target '/usr/lib/libfreeimage.so', needed by 'lib/libSMDS.so'.  Stop.

    # Fix with this line.
    sudo ln -s /usr/lib/x86_64-linux-gnu/libfreeimage.so /usr/lib

Once the build is complete, a runnable copy of the FreeCAD executable will be in the ``freecad-build`` folder. Any changes
made to the source code can be tested after re-compiling the executable.

Hopefully this post helps someone out there! Even if you are only contributing to the documentation as you learn FreeCAD,
your contribution is valuable and can help tons of people across the globe.
