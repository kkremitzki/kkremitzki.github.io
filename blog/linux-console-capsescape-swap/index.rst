.. title: Linux Console Caps/Escape Swap
.. slug: linux-console-capsescape-swap
.. date: 2016-05-17 22:40:12 UTC-05:00
.. tags: linux,raspberry_pi
.. category: 
.. link: 
.. description: 
.. type: text

Full-fledged Linux desktop environments like GNOME or Ubuntu's Unity often have built-in keyboard mapping tools to meet user needs.
At a lower level, ``xmodmap`` can be used to directly modify the X11 server's keyboard mapping. 
However, when working directly in the Linux console, things are a little more complicated without a display server.

My particular need is to swap the ``Caps Lock`` and ``Escape`` keys; as a ``vim`` user, I use ``Escape`` constantly to return to Normal mode.
To be more efficient and avoid the possibility of repetitive strain injury from long-term pinky stretching to reach ``Escape``, the following line
can be added to the file ``/etc/rc.local``, before the final line ``exit 0``.

.. code-block:: bash

  /usr/bin/dumpkeys | /bin/sed 's/CtrlL_Lock/Escape/' | /usr/bin/loadkeys

If you aren't familiar with Bash, a little explanation might be in order. First, note that this single-line command is actually three
commands separated by the pipe character ``|``. 
A detailed explanation can be found in the `Advanced Bash Scripting Guide's chapter on I/O Redirection
<http://www.tldp.org/LDP/abs/html/io-redirection.html>`_, but in short,
piping ``cmd1 | cmd2`` sends the output of ``cmd`` as input for ``cmd2``.

The programs ``/usr/bin/dumpkeys`` and ``/usr/bin/loadkeys`` are fairly self-explanatory: they output keymaps for the console
at the kernel level, and update that keymap if a valid file is input, respectively. 
The middle command, ``sed``, is a powerful, general-purpose stream editor, and the source of much Linux wizardry. To understand what it's doing,
take a look at its argument: the string ``'/s/CtrlL_Lock/Escape/'``. This tells ``sed`` to *s* ubstitute the first instance of ``CtrlL_Lock``
with ``Escape`` on any matching line from its input (adding ``g`` after the last slash makes it a truly global substitution and not linewise.)
The ``sed`` command then passes along the modified stream to ``loadkeys``. Because this line is added to ``/etc/rc.local``, it will be executed
every boot, swapping ``Caps Lock`` and ``Escape`` in the Linux console.
