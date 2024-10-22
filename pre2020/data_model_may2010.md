# Data Model (May 2010)

This page tries to capture the data & logic in the data model underlying
Getting Things GNOME!, which is similar & different in important ways
from other software that also use the concepts of *tasks* and *events*.
For the moment it is only *descriptive*, but in the future it may become
*normative*.

[This spreadsheet](http://spreadsheets.google.com/ccc?key=0AhRkDXhnjLt8dHM3MmZ0YmJnMm1UM1hySFNlaDBVc1E&hl=en_GB)
contains an easier-to-read, side-by-side comparison of the GTG data
model with other tools.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
"SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" are to be
interpreted as described in <http://tools.ietf.org/html/rfc2119>.

## Tasks

Every task MUST have the following properties:

- State
- Title
- Modification Time
- Content
- ID
- UUID

Additionally, a task MAY have the following properties:

- Completion Date
- Due Date
- Start Date

A task MAY also have one or more of the following:

- Tags
- Subtasks

### Mandatory properties

#### State

The *State* MUST be one of:

- Active
- Dismissed
- Done

If the *State* is 'Done', then a *Completion Date* MUST be given.

#### Title

The *Title* is a Unicode string, with no maximum length. It MUST NOT
contain the tab (\\t) or newline (\\n) characters.

#### Modification Time

A time without time zone, which MUST be specified to the nearest second.

#### Content

The Content of the task is a Unicode XML fragment which MAY have zero
length.

#### ID

The task ID is specified as a Unicode string in the format "A@B", where
both A and B are integers. The ID MUST be unique in any collection of
tasks.

#### UUID

The task UUID is a verision 4 UUID as specified in RFC 4122
\[<http://tools.ietf.org/html/rfc4122>\]

### Optional Properties

#### Completion Date

The Completion Date represents the date the Task was completed, and MUST
be specified as a day, month and year.

#### Due Date

The Due Date represents the user's target date for completing the task.
It may be specificed in the same form as the Completion Date, or as:

- Soon, or
- Later.

The date 'Soon' SHOULD be represented to the user as the string "Soon"
or its equivalent in the current locale. For the purposes of comparison
with other dates, 'Soon' SHOULD be taken to represent the a day 15 days
after the current day. The date 'Later' SHOULD be represented to the
user as the string "Later" or its equivalent in the current locale. For
the purposes of comparison with other dates, 'Later' MUST be taken to
represent the maximum date representable by the Python datetime object,
i.e. 31 December 9999
\[<http://docs.python.org/library/datetime.html#datetime.date.max>\].

#### Start Date

The Start Date represents a date after which the task may be worked on.
It MUST be specified using one of the forms valid for the Due Date.

### Multiple Properties

#### Tags

Each Tag is a reference to a Tag object

#### Subtasks

Each Subtask is a reference to another task, referred to as a "child" of
the current task. The reciprocal relation, of the parent task to the
child task, is called "parent". A Task MAY have any number of Subtasks.
A single Task MAY be a Subtask of multiple other Tasks.

## Tags

A tag MUST have a Name. It MAY have a Colour and Parent.

### Name

The Name MUST NOT contain whitespace or the comma character (,). The
first character of a tag Name MUST be "@".

### Colour

The Colour MUST be a representation of an 8-bit RGB colour, used to
represent the tag in user interfaces.

### Parent

Each Parent is a reference to another tag.

## Other GTG Concepts

### 'Started'

Any task is *started* which has the *State* 'Active' and:

- has a Start Date earlier than or equal to the current date, or
- has no Start Date.

### 'Workable'

Any task is *workable* which:

- has no Subtasks, or
- has only Subtasks with the State 'Done' or 'Dismissed'.

## Other Models & Software

### iCalendar

- <http://tools.ietf.org/html/rfc5545>

The iCalendar spec includes VTODO and VJOURNAL calendar components.
Shared properties are indicated in the accompanying spreadsheet. VTODO
includes the following notable properties that are not in the Task data
model:

- attach: file attachments, references to MIME parts or URIs.
- created: creation date/time.
- duration: can be specified instead of (not with) a due date.
  Duration must occur with
- geo, location: latitude-longitude and plain-text locations for the
  item.
- organizer: other user who is organizing the item.
- partstat: Participation state (of the current user in the current
  VTODO) NEEDS-ACTION, ACCEPTED, DECLINED, TENTATIVE, DELEGATED,
  COMPLETED, IN-PROCESS
- percent: percentage completion, as an integer.
- priority: integer 1-9, 1 being high.
- exdate,rdate,recurid,rrule,rstatus,seq: for specifying recurrence.
- url: locator for relevant information.

Notably absent is any form of hierarchy.

### Hamster

- <http://git.gnome.org/browse/hamster-applet/tree/src/hamster>

Has already done a client-server separation:
<http://projecthamster.wordpress.com/2010/04/30/experimentation-with-real-data/>

- Stores 'start_time' and 'end_time' but also a Python timedelta
  'delta', and returns in seconds as part of the DBus API — presumably
  for speed.
- No concept of modification, creation, deletion, state — simpler
  state model, user doesn't directly modify recorded facts.
- No concept of "due" dates: only records past/present activity.

### Zeitgeist

- <http://bazaar.launchpad.net/~zeitgeist/zeitgeist/trunk/files/head:/zeitgeist/>

Zeitgeist is the service counterpart to GNOME Activity Journal. The
Event class is the nearest analogue to a Task. Events have no concept of
duration; they are instantaneous. Key additional concepts include:

- 'Interpretation' of Events: "what happened".
- 'Manifestation' of Events: "how it happened", for example, through
  user activity, automatically via software, etc.
- 'Actor': software emitting the Event; in the case of tasks, possibly
  always GTG?

Both the *Interpretation* and *Manifestation* are stored as URIs, as in
XML DTDs.

### GNOME Planner

- <http://git.gnome.org/browse/planner/plain/examples/kitchen.planner>

Planner implements a Gantt-type task model. As a forward-looking,
planning tool, it has no concept of a difference between a Due Date and
a Completed Date (late execution). Subtasks are indicated (in the XML
backend) by hierarchy of the XML document, but differ from the non-GTG
concept of 'predecessors'. A predecessor is a task that must be
completed before another task can be started.

### Remember The Milk

- <http://www.rememberthemilk.com/services/api/tasks.rtm>

Additional concept of Task Series, which share certain properties.
Additional properties:

- Created: creation date/time.

- Estimate: estimated duration in days, hours or minutes.
- Priority: 1-3, 1 being highest.
- Postponed: amount of postponement of original due date, in days.
- Deleted date (deleted tasks are not removed; akin to 'Dismiss' in GTG)
- Recurrence: use of 'rrule' seems to indicate this is implemented
  according to the iCalendar spec
  \[<http://www.rememberthemilk.com/services/api/methods/rtm.tasks.setRecurrence.rtm>\]
- URL: per iCalendar.

Notably absent is the concept of a start date.

### Others

- GNOME Tracker uses
  \[<http://projects.gnome.org/tracker/features.html>\] the "Nepomuk
  CALendar ontology"
  \[<http://www.semanticdesktop.org/ontologies/ncal/>\]. Lots of
  documentation, no examples.

