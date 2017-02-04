.. title: Equation Solving with Python & SymPy
.. slug: equation-solving-with-python
.. date: 2016-04-10 06:12:16 UTC-05:00
.. tags: mathjax,python
.. category: 
.. link: 
.. description: 
.. type: text

In engineering applications, the same equation will be solved over and over with 
different values or measurements as inputs. Anticipating this, we can either 
write one function for each variable which inputs all other variables, or take a 
much easier route using SymPy_.

The following example is a simple implementation of `Manning's formula <https://en.wikipedia.org/wiki/Manning_formula>`_:

\\[
v = \\frac{k}{n} {R_h}^{2/3} S^{1/2}
\\]

with :math:`k = 1.49` since we most often work in English units in American 
hydrology. Note that the variable ``mannings_eqn`` is actually the above 
expression set equal to 0, so that we see a :math:`-v` term.

The following code creates Sympy ``Symbol``\s for each variable in the expression. 
In general, if we have :math:`n` variables in the expression, we can pass in a 
``dict`` with :math:`n-1` key-value pairs (equations) with known values
to solve for the :math:`n`\th variable. We can create ``dict``\s with keys, the 
set of knowns, and pass in any (independent) combination of :math:`n-1` variables from
our expression to get a number.

.. TEASER_END

.. code-block:: python

  from sympy import symbols, solve

  v, n, Rh, S = symbols('v, n, Rh, S')

  knowns_1 = {n: 0.025, Rh: 10, S: 0.01}
  knowns_2 = {v: 100, n: 0.01, S: 0.05}
  knowns_3 = {n: 0.05, Rh: 5}

  def solve_mannings(input_dict):
      mannings_eqn = -v + 1.49/n * Rh**(2/3) * S**(1/2)
      # Use dict flag to get {variable: value} output, not anonymous [value]
      solution = solve(mannings_eqn.subs(input_dict), dict=True)
      print(solution)

  solve_mannings(knowns_1)
  solve_mannings(knowns_2)
  solve_mannings(knowns_3)

However, the third set of knowns gives us an 
`underdetermined system <https://en.wikipedia.org/wiki/Underdetermined_system>`_ 
since we only have two equations for our four-variable system. Accordingly, we 
will have as output one variable as a function of another, in this case :math:`S`:

.. code-block:: python

  [{v: 27.6638694483322}]
  [{Rh: 5.19987727958683}]
  [{v: 87.1357285987434*sqrt(S)}]

.. _SymPy: http://www.sympy.org/en/index.html

