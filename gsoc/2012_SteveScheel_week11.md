# Week 11 Report

I am happy to announce that I have the task editor working inside of
GTG! That was the big breakthrough in the past week. However, it isn't
perfect yet, because for some reason using the Gtk Window method
present() to bring a window up and into focus stops working properly
after an editor has been closed (which if you would like to test just
grab the latest code and run GTG. Open a task then close it and try
opening up tasks, the placement will be weird and not on top or in focus
as it should be). I also figured out how to get button labels working
properly so now the GUI is much closer to the proposed one in the design
docs on the Wiki.

