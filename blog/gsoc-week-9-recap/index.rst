.. title: GSoC Week 9 Recap
.. slug: gsoc-week-9-recap
.. date: 2017-08-10 21:18:04 UTC-05:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text

I celebrated my birthday in south Texas last week! I was about 3 miles from the future SpaceX launch facility opening in 2018. 
It'll be great to possibly see launches to Mars from there in the next few years.

I mostly spent this week working on the bugs I mentioned last week. I wanted to try to make a dent in the outstanding bugs I've found.
Unfortunately, my lack of C++ background (compared to Python) really hampered this; it's a little bit like trying to run before you walk.
In the end, I only fixed the Revolution bug(s). In the case where a revolution is attempted on the same plane as the sketch, resulting in e.g. a flat disc,
the issue was that the code was checking the angle between the sketch's normal and the revolution plane's normal, looking for a 0° angle. However,
it was failing to fail in the case of a 180° angle.

I also added a simple convenience check for all tools in Part Design: if you open a document with only one body and try to click a PDN tool's button,
the single body will be auto-activated instead of popping up a warning. If there are no bodies or more than one, the warning still occurs.
