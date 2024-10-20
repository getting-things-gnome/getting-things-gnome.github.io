# Creating and manipulating Trees and Nodes

***Liblarch API: 1.0***

In liblarch, your data structure is always a tree. Even if you want to
make a simple list, it is implemented by a tree. You can control the
limitations of your tree by removing the right for nodes to have parents
or to have children.

Every element of your data structure is a node (here, the coloured
circles). You build your tree by adding nodes to the tree and creating
relationships between the nodes. If you don't create any relationships,
you will have a flat list (drawing nbr 1).

![](http://ploum.net/publique/ploum.net/liblarch/liblarch1.png "http://ploum.net/publique/ploum.net/liblarch/liblarch1.png")

Creating a tree is easy:

```python
from liblarch import Tree

my_tree = Tree()
```

Liblarch manipulates "[TreeNodes](/TreeNodes)". You can define your own
objects but they have to extend the liblarch.tree.[TreeNode](/TreeNode)
class. [TreeNode](/TreeNode) are initialized with a Node ID parameter
(nid). The nid is a string that should be unique. No nodes can have the
same nid in a given tree.

```python
from liblarch import TreeNode

class MyObject(TreeNode):

    def __init__(self, myparameter, unique_id):
        TreeNode.__init__(self, unique_id)
        self.parameter = myparameter
```

all you need to do afterward is to add nodes to your tree

```python
node1 = MyObject("parameter","node1")
my_tree.add_node(node1)
```

A particularity of Liblarch is that it is asynchronous. If you create a
relationship between node C and F and one of the node is not in the
tree, that relationship is saved for later and created only when both
nodes are presents.

## Tree object

Concepts of Filters and Views are [explained later](viewtree).

| Function | Description |
|----------|-------------|
| `__init__(self)` | Return a new empty tree |

### Nodes

| Function | Description |
|----------|-------------|
| `get_node(self, node_id)` | returns the node object corresponding to the nid |
| `has_node(self, node_id)` | returns True if a node_id node exists in the Tree, False otherwise |
| `add_node(self, node, parent_id=None, priority=None)` | add the node to the tree. If parent_id is given and a node currently in the tree, then node is added as children of parent_id. If parent_id is given but doesn't exist, node is added to the root of the tree but, if a node with parent_id appears later, node will be moved accordingly. Priority is either "high", "normal" or "low" and affects how fast should liblarch handle the request. |
| `del_node(self, node_id, recursive=False)` | Remove node node_id from the tree. Return True if successfully removed. Recursive=True implies that all children and sub-children of node_id will also be removed |
| `refresh_node(self, node_id, priority="low")` | Tell liblarch that the node was modified. Priority is either "high", "normal" or "low". |
| `refresh_all(self)` | Refresh all nodes |
| `move_node(self, node_id, new_parent_id=None)` | Move the node to a new parent (dismissing all other parents) |
| `add_parent(self, node_id, new_parent_id=None)` | Add the node to a new parent. Return whether operation was successful or not. If the node does not exists, return False |

### Views

| Function | Description |
|----------|-------------|
| `get_main_view(self)` | Return the special view "main" which is without any filters on it. |
| `get_viewtree(self, name=None, refresh=True)` | Returns a viewtree. If a viewtree with that name exists, return it. Else, create it and return it. If name is None, create an anonymous tree (do not remember it). If refresh is False, the view is not initialized. This is useful as an optimization if you plan to apply a filter. |

### Filters

| Function | Description |
|----------|-------------|
| `list_filters(self)` | Return a list of all available filters by name |
| `add_filter(self, filter_name, filter_func, parameters=None)` | Adds a filter to the filter bank. Return False if a filter with that name already existed in that bank. |
| `remove_filter(self,filter_name)` | Remove a filter from the bank. Only custom filters that were added here can be removed. Return False if the filter was not removed. |


## TreeNode object


| Function | Description |
|----------|-------------|
| `__init__(self,node_id, parent=None)` | Create a node with the name node_id. If parent is given, it should be a TreeNode object. |
| `get_id(self)` | Return node_id |
| `modified(self,priority="low")` | Force to update node (because it has changed). Priority is either low, medium or high |
| `get_tree(self)` | Return associated tree with this node |

### Parents

| Function | Description |
|----------|-------------|
| `set_parents_enabled(self,bol)` | If bol is True, the TreeNode is allowed to have parents. Else, it will always be at the root. |
| `has_parents_enabled(self)` | return whether or not the node is allowed to have parents |
| `add_parent(self, parent_id)` | Add a new parent to the node, by its node_id |
| `set_parent(self, parent_id)` | Remove other parents and set this parent as only parent, by its node_id |
| `remove_parent(self, parent_id)` | remove a parent with its node_id |
| `has_parent(self, parent_id=None)` | Return True if node has at least one parent. If parent_id is given, returns if there's a parent with that node_id. |
| `get_parents(self)` | Returns the node_id of the parents of the current node |

### Children

| Function | Description |
|----------|-------------|
| `set_children_enabled(self,bol)` | |
| `has_children_enabled(self)` | |
| `add_child(self, child_id)` | |
| `has_child(self, child_id=None)` | True if node has at least one child. if child_id is given, check only if there's a child with that node_id |
| `get_children(self)` | Return node_id of children of the node|
| `get_n_children(self)` | Return count of children (int) |
| `get_nth_child(self, index)` | Return the nth child |
| `get_child_index(self, node_id)` | |

