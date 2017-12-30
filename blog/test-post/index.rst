.. title: Test Post
.. slug: test-post
.. date: 2026-02-28 13:01:42 UTC-06:00
.. tags: mathjax
.. category: 
.. link: 
.. description: 
.. type: text

Math samples:

Inline Euler’s formula: :math:`e^{ix} = \cos x + i\sin x`

LaTeX equation-type environment, inverse Fourier transform:

\\[ 
f(x) = \\int_{-\\infty}^\\infty
\\hat f(\\xi)\\,e^{2 \\pi i \\xi x}
\\,d\\xi
\\]

Python and JavaScript code samples.

.. code-block:: python3

    #!/usr/bin/env python

    from engine import RunForrestRun

    """Test code for syntax highlighting!"""

    class Foo:
        def __init__(self, var):
            self.var = var
            self.run()

        def run(self):
            RunForrestRun() # run along!

.. code-block:: javascript

    $(function() {
      var listItem, itemStatus, eventType;

      $('ul').on(
        'click mouseover',
        ':not(#four)',
        {status: 'important'},
        function(e) {
          listItem = 'Item: ' + e.target.textContent + '<br />';
          itemStatus = 'Status: ' + e.data.status + '<br />';
          eventType = 'Event: ' + e.type;
          $('#notes').html(listItem + itemStatus + eventType);
        }
      );

    });

