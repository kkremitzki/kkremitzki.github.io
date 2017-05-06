.. title: Primer on Python Projects
.. slug: primer-on-python-projects
.. date: 2016-04-10 07:58:54 UTC-05:00
.. tags: python
.. category: 
.. link: 
.. description: 
.. type: text

I'm helping all the teams in my BAEN370 class robotics competition (essentially our final) since I competed in the ASABE Robotics Competition last year in New Orleans.
This post is advice mainly targeted at everyone in the class.
Here are a few useful snippets when starting your first big Python project. 

.. class:: h3

Imports

If you're working on a file, e.g. ``code.py``, and it's getting large, you can break off some of that code (usually functions) into another file. Let's say you name this file ``functions.py``. Then, in your original file, you would add to the top:

.. code-block:: python
 
 from functions import function1, function2 # etc
 # if you have a lot of functions, you can use something like
 # from functions import (function1, function2, ... ,
 #                        functionN_minus_one, functionN)

An example of how to use this, in the context of BAEN370, would be using the following project structure:

::

  baen370/
  ├── run.py
  ├── navigation.py
  └── sensors.py

Then, those files' contents would look something like this:

.. TEASER_END

**run.py**

.. code-block:: python
  
  from navigation import NavigationStrategy
  # Add more imports like this if you need something from sensors.py, etc.

  if __name__ == '__main__':
    # Bundle your code for how to handle the maze into one function.
    # That way you can have a file just for running the maze, and you
    # can work on other functions by themselves in logically separated files.
    NavigationStrategy()    


**navigation.py**

.. code-block:: python

  from sensors import front_prox, right_prox, front_far

  def NavigationStrategy():
    # Describe your navigation strategy here.
    # It might look something like this, if you're doing a right-following strategy
    while True:
      while front_far() and right_prox():
        if not front_prox():
          # gotta go fast
        else:
          # slow it down
      while not right_prox():
        # How will you handle a right proximity sensor saying "there's no wall nearby"?


**sensors.py**

In this example, I could have used ``from gopigo import *``, but this is discouraged. For more on why, check out http://stackoverflow.com/a/2360808.

.. code-block:: python

  import gopigo as gpg
  # Don't do this:
  # from gopigo import *

  # Set your thresholds for what is "close" and "far" here
  near_threshold = 15 # cm, assuming sensors' voltage->cm math is true
  far_threshold = 50 # cm

  def front_prox():
    # write a function that looks like
    if some_condition #  sensor says stuff is near
      return True
    # No need for else here
    return False

  def right_prox:
    # something similar to front_prox. replace "pass" with the definition of the function
    pass

  def front_far:
    # If you want to try to speed up in a straightaway, 
    # write something that returns True when it should go fast
    # Replace "pass" with your code.
    pass


.. class:: h3

Using IDLE

IDLE is not the best tool for the job (I'd recommend the free IDE, Spyder) but if it's the tool you use, you might as well get the most out of it.
Here are a few useful keyboard shortcuts

- ``Alt-P`` and ``Alt-N`` in the interpreter pull up your **P** revious and **N** ext commands, respectively.
- ``Ctrl-[`` and ``Ctrl-]``  decrease and increase the level of indent of a region
- ``Alt-3`` and ``Alt-4`` comment and uncomment a highlighted region. You can also surround a region by triple apostrophes or triple quotes to make it a multi-line string (which is also a multi-line comment in Python.)


.. class:: h3

Useful Builtins 


Whenever you see ``>>>`` (triple chevrons), you're in the `Python interpreter
<https://docs.python.org/2/tutorial/interpreter.html>`_. This environment is very useful. You can inspect things in the code you've already ran, write new functions, test out code, and generally use the full power of Python.
One of the first steps to unleashing this power is learning about the `builtin functions
<https://docs.python.org/2/library/functions.html>`_. I'll highlight a few useful tools.

``help()``
  Try running ``help(help)`` yourself to see the following description.
  This is a wrapper around pydoc.help that provides a helpful message
  when 'help' is typed at the Python interactive prompt.
  Calling help() at the Python prompt starts an interactive help session.
  Calling help(thing) prints help for the python object 'thing'.

        
``dir()``  
  Use this command to show all the names accessible in a thing. If you call it without an argument, like ``dir()``, it shows you everything accessible in the current scope. 
  For example, if you do ``import math``, then ``dir()`` will show a list of all names you have accessible, including ``math``. If you type ``dir(math)``, you will see everything
  accessible under ``math.<thing>``, e.g. ``math.sin``, ``math.log``. Try it out!

``len()``
  Returns the number of items in a container. For example, if you have a ``list`` where ``x = [0, 1, 2]``, then typing ``len(x)`` will return ``3``. 

``_``
  The underscore symbol is a useful bit of shorthand that refers to the last thing you typed. 
  For example, if you're using the Python interpreter as a calculator and you're trying to solve some expression with a complicated numerator and denominator, it can be easier to do one or the other first, and then refer to it as ``_`` in the subsequent calculation.
