# Viewing and Filtering your Tree

***Liblarch API: 1.0***

For each liblarch Tree, you can create as many View as you want. In
liblarch, those are called "ViewTree" (not to be mixed with
the gtk.TreeView widget). The advantage is that each View
can be filtered.

A liblarch Filter is simply a function that take a TreeNode
as a parameter and return True if the Node should be displayed with the
filter, False otherwise.

In order to be used in a given ViewTree, fiters have to be
added with an unique name to the Tree. The Tree acts as a filter bank,
allowing each ViewTree to use all the filters currently in
the bank.

EXAMPLE: creating a filter, adding it to a tree, creating a viewtree,
applying a filter to it.

## ViewTree

### Filters

A filter is a predicate which decides if node should be shown or hidden.
Example of such a filter which displays only active tasks in Getting
Things GNOME! is:

```python
def is_active(node):
    return node.get_state() == "active"
```

Filters can have parameters. It prevents you creating the same filter
again and again. In Getting Things GNOME! the user can have many gtags.
When she filters tasks by a tag, we apply a general filter with the tag
as the parameter:

```python
def has_tag(node, parameters):
    tag = parameters['tag']
    return tag in node.get_tags()
```

A flat filter is a special filter. If applied, the final tree will be
flat -- just list of nodes. When you want to show tasks which you
completed the last week, a float filter is applied because you are not
interested in relationships among them. One flat filter is enough to
produce list instead of a tree. A flat filter has set parameter 'flat'
to True.

A transparent filter is another special filter. It provides you an
option to count nodes with all applied filters or only with
non-transparent filters.

Let have the following situation: There is a filtering pane which shows
the name and the count of nodes for filter. The user chooses a filter
and a view is updates. Afterwards the counts of tasks for filters has
changed. You do not want to do that. You want to "ignore" the last
filter and count without it. There might be a situation when you want to
count it. Therefore every time you can choose to use or ignore
transparent filterswhen counting.

