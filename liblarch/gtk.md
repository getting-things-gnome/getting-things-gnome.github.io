# GTK widget for liblarch

***Liblarch API: 1.0***

liblarch-gtk allows to connect a liblarch.ViewTree to a
gtk.TreeView. All you have to do is define how you will
display your data.

More to come

LibLarch's TreeWidget displays a view in a
TreeView. Every time the view is changed, the
TreeView is also updated. In fact, LibLarch
TreeWidget is pre-configured TreeWidget.

To construct LibLarch Widget you need to pass a
ViewTree and description of columns to display. A
definition of a column is a dictionary where keys are:

- value (required) => (type of values, function for generating value from a node)
- renderer (required) => (renderer_attribute, renderer object)
- order => specify order of column otherwise use natural oreder
- expandable => is the column expandable?
- resizable => is the column resizable?
- visible => is the column visible?
- title => title of column
- sorting => allow default sorting on this column
- sorting_func => use special function for sorting on this func

LibLarch TreeWidget has support for Drag and
Drop, background color and selections.
