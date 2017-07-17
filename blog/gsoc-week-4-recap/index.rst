.. title: GSoC Week 4 recap
.. slug: gsoc-week-4-recap
.. date: 2017-06-30 05:48:06 UTC-05:00
.. tags: gsoc,freecad
.. category: 
.. link: 
.. description: 
.. type: text

I started this week out with the goal of troubleshooting the bugs I found with PartDesign Pipe and Revolve.
However, I ended up running into several annoying issues. The LLDB debugging integration I previously wrote about
began showing some inexplicable errors::

    error caught in async handler 'exec ('continue',)'
    Traceback (most recent call last):
      File "/home/kurt/.config/nvim/bundles/repos/github.com/dbgx/lldb.nvim/rplugin/python/lldb_nvim/__init_
    _.py", line 49, in _exec
        self.ctrl.safe_execute(args)
      File "/home/kurt/.config/nvim/bundles/repos/github.com/dbgx/lldb.nvim/rplugin/python/lldb_nvim/control
    ler.py", line 101, in safe_execute
        self.safe_call(self.exec_command, [cmd])
      File "/home/kurt/.config/nvim/bundles/repos/github.com/dbgx/lldb.nvim/rplugin/python/lldb_nvim/control
    ler.py", line 94, in safe_call
        raise EventLoopError("Dead event loop!")
    EventLoopError: Dead event loop!

Eventually I found `an issue on Github <https://github.com/dbgx/lldb.nvim/issues/52>`_ which refers to
a now-deleted comment in the author's original repository, stating the project was no longer being developed.
The question remains as to how it was working just fine when I began and only just now stopped working, but
the end result was that my debugger-editor integration was broken, which makes it quite a bit tougher to debug
the C++ side of the codebase.

One option I had was to just use GDB as a standalone command line application, but it's really convenient, e.g.
to not have to manually type out file names and line numbers for breakpoints, and otherwise have your debugger
wired up to your editor.

However, this was inexplicably not working either! Basic features of GDB worked, but trying to specify breakpoints
to step through the code was not. I banged my head on this issue for a while until I figured up ``ccmake`` to
take a look at my build options. The issue? Somehow, the ``CMAKE_BUILD_TYPE``, which had been set to ``Debug``,
was unset. So, I set it again and started the debug build, which takes quite a long time. 
(Around 2 hours with ``make -j4``.)

I also did more research on options for debugger integration. I found an interesting option called Pyclewn
which is a debugger front-end for (neo)vim. This option was attractive since I could have a unified front-end
to both my C++ debugger as well as a Python one. However, setup wasn't straightforward, so I continued searching
for a simpler option.

Luckily, I stumbled upon `neovim_gdb.vim <https://github.com/neovim/neovim/blob/master/contrib/gdb/neovim_gdb.vim>`_,
a simple combination of vim settings, available in the ``contrib`` folder of the neovim repository.

Once that was taken care of, I started working on my original objective for the week. I found that the
PartDesign Pipe issue was being caused by the code checking for whether or not the Pipe's AuxillerySpine (sic)
was a part of the active body, but didn't check if the thing existed first. This resulted in a check to
see if a null pointer was part of the active body, which is never the case. Checking for existence first
`resolved the issue <https://github.com/FreeCAD/FreeCAD/pull/848>`_. With that bug fixed, I also added
two tests each for PartDesign Pipe and Loft.


+----------------------------------+-----------------------------+-----------+-----------------------------+
| tool category                    | initial, current test count |  status   | notes                       |
+==================================+=============================+===========+=============================+
|  datum tools                     |            0, 0             |   ready   |                             |
+----------------------------------+-----------------------------+-----------+-----------------------------+
|  add. & sub. features/primitives |           11, 15            |   ready   | all additive & subtractive  |
|                                  |                             |           | features now have at least  |
|                                  |                             |           | one test                    |
+----------------------------------+-----------------------------+-----------+-----------------------------+
|  transformations                 |            3, 3             |   ready   |                             |
+----------------------------------+-----------------------------+-----------+-----------------------------+
|  dressup features                |            0, 0             |   ready   |                             |
+----------------------------------+-----------------------------+-----------+-----------------------------+
|  boolean operation               |            0, 0             |   ready   |                             |
+----------------------------------+-----------------------------+-----------+-----------------------------+
