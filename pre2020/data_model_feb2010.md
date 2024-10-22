# Data Model (February 2010)

What is a task, a tag? This page may help!

# Task

Class:
- id (string ?)
- uuid (uuid)
- content (string)
- sync_func (?)
- title (string)
- status (Active, Done, Dismiss, None)
- closed_date
- due_date
- start_date
- parents (array of parents id) (?)
- children (array of children id)
- can_be_deleted ("newtask" ?)
- tags (array of tags)
- req ("requester" \<= user ?)
- loaded (? contains newtask or id)
- attributes (array of ?)
- other ?

XML (utf-8):

- id (in the form 1@1 or 2@1 or 3@1, what is the '@1' part ?)
- status
- tag list
- uuid
- title (text)
- modified (date)
- duedate (date)
- content (big text)
- subtask

# Tag

- name (unique, string, begins with "@")
- color (string(7), begins with #, html color format)
- other ?

# TagStore

- contains a list of existing tags

