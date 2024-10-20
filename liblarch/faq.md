# General FAQ about Liblarch

## Why libLarch?

In Getting Things GNOME! we tackled constraints of
TreeWidget. It was designed to manage trees. Tree is a
graph structure where every node except the root node has just one
parent and it is a root of several subtrees.

Getting Things GNOME! supports tasks which have more parents -- directed
acyclic graph. In the end we want to display tasks in a form of tree
which is more natural for humans.

libLarch manages directed acyclic graphs internally and represents them
in other form, e.g. trees.

Filtering tasks is one of biggestadvantages of Getting Things GNOME!
Filters show only nodes which satisfy a condition like "has tag
@to_buy". Combining several filters you get tasks you want, e.g. every
work-related task which I completed the last week.

We again tackled constrants of TreeWidget: if a parent is
hidden, children can't be shown. TreeWidget does not
allow you to specify which nodes you want to show by a simple function.

libLarch encapsulates these details and let you spend the saved time on
other aspects of your application.

## Why is it called libLarch?

Well, at first, liblarch was created to handle the particular trees used
by GTG. And what's a huge tree you can recognize from quite a long
distance? The [larch](https://en.wikipedia.org/wiki/Larch), obviously.
Hence libLarch.
