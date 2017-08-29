.. title: GSoC Week 10 Recap
.. slug: gsoc-week-10-recap
.. date: 2017-08-20 07:22:49 UTC-05:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text

The final portion of GSoC for me will be dedicated to working on improvements to the Attachment Editor, and this post will essentially be my design
for what those improvements will look like. The Attachment Editor is available in the Part Workbench through Python. One can for example create a simple
Part Cube, select it, then click Part -> Attachment. It also is used when creating datum geometry in Part Design, or when creating a primitive.

Here are a few screenshots:

.. figure:: /images/gsoc-10-1.png
  :align: center
  :alt: command palette

  Figure 1. The Python-based Attachment Editor in the Part workbench.

.. figure:: /images/gsoc-10-2.png
  :align: center
  :alt: command palette

  Figure 2. Creating a Datum Plane.

Creating datum geometry is a key part of the Part Design process, so it's helpful for it to be very easy and intuitive. The current
Attachment Mode information especially can be quite overwhelming to a beginner, however. Especially considering how improvements
to the Attachment Editor could be reused in a future Assembly Workbench, it was decided to look into improving these tools.

The first, most obvious improvement here would be inactivating the "Extra placement" section when inactive. This could
possibly be accomplished by making a separate collapsible section which automatically hides when there is no attachment.

The second, and tougher improvement, involves reworking the current the four attachment selections and the attachment mode.
Reference names probably don't need to be more than 3/4ths the width of the page. The methods for selecting references via
an activation button, and deleting via clearing out the text are not user-friendly. 

The four-reference list here would ideally be replaced with an icon-based grid, which starts out empty. Each selection's icon would
be based on its type, e.g. Vertex, Edge, Face, Curve, etc., where available, and a generic icon for unrecognized types. The selection's name
could be displayed in a shortened form, e.g. "MyLongShapeNameIs...". This approach could be extended for future Assembly use by adding a scrollbar
on the icons, allowing for several rows of attachment references, 4 at a time.

This tool could be very user-friendly, as invalid reference icons can be highlighted red, and when the attachment is complete, the reference set's icons
can be highlighted green. Ghosted icons can be displayed as needed for a selected Attachment Mode.

A similar approach for Attachment Mode could be used. Using a 4-icon row with a scrollbar, attachment modes can be explained with a short label and
an icon, where feasible; hopefully the large size will allow for expressive icons. When a mode is moused over or selected, the remaining references required
can be displayed in the reference selection area.

Altogether, (i) splitting out the placement and toggling when it has no effect (i.e. there is no attachment) and (ii) reworking Reference Selection and Attachment Mode
dialogs to use unified icon list GUI code, as well as (iii) making the icon set to explain the attachment concepts to users, comprise the components of this
"Attachment Editor Improvement" project.
