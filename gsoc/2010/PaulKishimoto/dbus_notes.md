Some notes on things that will eventually become DBus calls in GTG:

## Calls on GTG.core objects from within the GTK UI

- GTG/gtk/
  - dbuswrapper.py:
    - Requester.
      - delete_task()
      - get_task()
      - has_task()
      - new_task()
    - Task.
      - add_child()
      - add_tag()
      - get_children()
      - get_closed_date()
      - get_due_date()
      - get_start_date()
      - get_id()
      - get_parents()
      - get_status()
      - get_tags_name()
      - get_text()
      - get_title()
      - set_due_date()
      - set_start_date()
      - set_status()
      - set_text()
      - set_title()
  - delete_dialog.py:
    - Requester.
      - delete_task()
      - get_task()
    - Task.
      - get_subtasks()
  - manager.py:
    - Requester.get_task()
  - browser/
    - browser.py:
      - Requester.
        - apply_filter()
        - connect()
        - get_all_tags()
        - get_custom_tasks_tree()
        - get_main_n\_tasks()
        - get_new_task()
        - get_task()
        - has_task()
        - reset_tag_filters()
        - unapply_filter()
      - Tag.
        - get_attribute()
        - set_attribute()
        - del_attribute()
      - Task.
        - STA_ACTIVE
        - STA_DISMISSED
        - STA_DONE
        - add_child()
        - add_tag()
        - get_id()
        - get_self_and_all_subtasks()
        - get_status()
        - get_tags()
        - get_tags_name()
        - get_title()
        - set_due_date()
        - set_start_date()
        - set_status()
        - set_title()
        - set_to_keep()
        - set_tooltip_text()
        - sync()
    - tagtree.py:
      - Requester.
        - get_main_tasks_tree()
        - get_tag()
        - get_tag_tree()
        - get_task()
        - rename_tag()
      - Tag.
        - get_attribute()
        - get_name()
      - Task.
        - add_tag()
        - get_tags_name()
        - remove_tag()
        - sync()
    - tasktree.py: imports GTG.core.tree.Tree and .TreeNode but doesn't use them.
      - Requester
        - get_task()
      - Task.
        - STA_ACTIVE
        - STA_DISMISSED
        - add_parent()
        - get_closed_date()
        - get_days_left()
        - get_due_date()
        - get_id()
        - get_parents()
        - get_start_date()
        - get_status()
        - get_tags()
        - remove_parent()
  - editor/
    - editor.py:
      - Requester.
        - connect()
        - delete_task()
        - get_used_tags()
        - new_task()
      - Tag.
        - get_name()
      - Task.
        - STA_DISMISSED
        - STA_DONE
        - add_child()
        - add_tag()
        - get_children()
        - get_closed_date()
        - get_days_late()
        - get_days_left()
        - get_due_date()
        - get_id()
        - get_start_date()
        - get_status()
        - get_subtasks()
        - get_tags()
        - get_tags_name()
        - get_text()
        - get_title()
        - has_tags()
        - is_new()
        - remove_child()
        - remove_tag()
        - set_closed_date()
        - set_due_date()
        - set_start_date()
        - set_status()
        - set_text()
        - set_title()
        - set_to_keep()
        - sync()
    - taskview.py:
      - Requester.
        - get_task()
        - has_task()
      - Task.
        - get_status() — compares with a string!
        - get_title()
        - set_title()

## Changes

- *Requester becomes the main DBus interface of the server*.
- *String representation of Task and Tag should be their most
  commonly-used property*.
  - `Task.get_id()` → `Task.__str__()`
  - `Tag.get_name()` → `Tag.__str__()`
- *Simple attribute access for DBus clients*: Use decorators,
  `__getattr__` and `__setattr__` in DBus Tag and Task proxy
  objects for properties like closed_date, due_date, start_date,
  status, text, title, etc.:
  - `d = task.get_closed_date()` → `d = task.closed_date`
  - `task.set_closed_date(d)` → `task.closed_date = d`
  - This will involve subclassing
    dbus.proxies.ProxyObject, which already has a custom `__getattr__`.
- *Simple collections as attributes for children, tags*
  - `task.has_tag('t')` → `'t' in task.tags` or similar
- *Eliminate duplication of concepts*: subtasks of a Task are
  sometimes addressed using the TreeNode idiom of
  "children".
- *Modify objects directly.* The server knows when the tree needs to
  be groomed/other objects updated:
  - `Requester.delete_task()` → `task.delete()`
  - `Requester.rename_tag()` → `tag.name = 'newname'`
- *Examine calls to `Requester.connect()`*: Requester is a subclass of
  gobject.GObject. Is it kosher to connect GObject signals across
  DBus? I can't imagine it is...
- *Replace unneeded functions*: `Task.is_new()`, `Task.set_to_keep()` seem
  to be here to support UI behaviours. Don't do these things at the
  level of the data model.
- *Eliminate object getters*...like `Requester.get_tag()` and
  `Requester.get_task()`. With canonical DBus paths, the client can just
  use `bus.get_object()` with the object ID to get the object directly,
  e.g. at:
  - /org/gnome/GTG/Store/Task/da7b144d-db6d-471d-97e8-d13a22c089e
  - /org/gnome/GTG/Store/Tag/todo

