# Getting Things GNOME! Web Service and API

The goal of this proposal is to add Getting Things GNOME! (GTG) web
service and API similar to Snowy for Tomboy. GTG is a standalone
application, which is good - because it does not require Internet
connection to work, but if a user has more than one computer and wants
to use GTG on them, (s)he will have to maintain separate lists of tasks.
Synchronization with a central server enables the user to access and
share their notes over multiple computers.

This service enables easy access to GTG tasks on any device. It
decreases the need for porting GTG to Internet enabled mobile platforms
(e.g. Android, iPhone/Pad, Symbian) because the service can be accessed
via browser or light html based apps. It enables synchronization of
tasks between GTG installations (between home and work computer or
desktop and laptop). Synchronization is also a fail-safe in case of a
hard drive failure.

Organizations or individuals could set up their own private instances of
the service or use the central GNOME hosted service - which would be
used by most users without their own servers. It would make GTG more
popular and it would have an advantage in comparison with other desktop
based to-do applications.

Core of the service will be similar to (and based on) Snowy, but with
new data models, views, templates and logic to be better suited for GTG
tasks and tags. It will add add a new API for GTG task synchronization.

### Use cases:

- Sanja is a GTG user who just bought a new laptop, she would like to
  have her GTG tasks both on her desktop and laptop.
- Bill uses GTG for his to-do needs. He would like to view his tasks
  on a cell phone when he's away from computer.
- James is a GNOME and GTG user at home, but works for a big company
  and has to work on other operating systems there. He uses the
  browser to manage his tasks using GTG Online, and they're there when
  he gets home.

### Midterm goal:

At midterm we would have a data model and API in GTG Online and also a
sync plugin in the desktop GTG so we could synchronize tasks between
them. There would also be a functional template and view for accessing
notes using a web browser.

### Timeline:

May 24 - May 30: Making a skeleton django app based on Snowy.

May 31 - June 13: Making a Django data model for GTG tasks. Basic views
for displaying data.

June 14 - June 27: Adding API templates and handlers for
synchronization.

June 28 - July 11: Adding GTG Online synchronization support to desktop
GTG.

**midterm**

July 12 - July 25: Adding editing capabilities and improving usability
of web view.

July 26 - Aug 8: Bug fixing, mobile web view.

Aug 9 - Aug 16: Fixing remaining bugs

# Details

## API

| Resource | URI | GET | PUT |
|----------|-----|-----|-----|
| User | api/user/ | Get basic user information, as well as references to its tasks and tags. | 
no PUT, users can't be created with API. |
| Tasks | api/user/tasks/ | List all tasks pertaining to a user, with references to individual notes. | 
Create, modify and delete tasks. |
| Task | api/user/tasks/id/ | Get a specific task. | No PUT. |
| Tags | api/user/tags/ | List all user's tags. | Create, modify and delete tags. |

#### domain/api/user/

replace user with actual username.  
Supported method - GET.  
GET returns:

- `username`
- `first_name`
- `last_name`
- References to tasks in api and web view.
- Reference to tags in api.

#### domain/api/user/tasks

Supported methods - GET, PUT.  
Supported parameter - `include_content` (boolean) defaults to `False`.  
GET returns a list of tasks with parameters:

- `id`
- `status`
- `tags`
- `uuid`
- `title`
- `duedate`
- `modified`
- `subtasks`
- `location`??? (or should we handle extra and future features, such as
  geo-locations differently?)
- `content` (content is displayed if `include_content` is set to `True`)
- References to this note in api and web view.

PUT uses the same parameters and adds an additional `delete` key. If
`delete` is set to `True`, the task is deleted. It returns a modified list
of tasks.

#### /domain/api/user/tasks/id

Supported method - GET.  
GET returns:

- `id`
- `status`
- `tags`
- `uuid`
- `title`
- `duedate`
- `modified`
- `subtasks`
- `location`??? (look above)
- `content`

#### domain/api/user/tags

Supported methods - GET, PUT.  
GET returns a list of tags with parameters:

- `name`
- `color`

PUT uses the same parameters and adds an additional delete key. If
delete is set to True, tag is deleted. It returns a modified list of
tags.

## Interface

A quick (really quick) mockup of the main interface, just to show what I
have in mind. Something between desktop GTG and gmail.

![Mockup](gsoc2010_jez_mockup1.png)

