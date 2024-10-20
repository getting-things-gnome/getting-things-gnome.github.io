# Proposed Data Model Changes (old)

Three categories of changes to the GTG data model must be considered:

- simplification of the current data model.
- adding fields common to other applications.
- adding fields particular to one other application or source.

These are considered in turn. For context, it is helpful to read a
synopsis of the [Getting Things Done concept](http://en.wikipedia.org/wiki/Getting_Things_Done).
GTG! is a GTD tool, so the distinctions are important.

## Simplifications

### Subtasks

Few other tools share the concept of subtasks, instead using tagging or
categorization to group tasks together. Planner is a notable exception,
especially because (as implied by the name) it is a *planning* tool,
using the [Gantt model](http://en.wikipedia.org/wiki/Gantt_chart). In
GTG!, subtasks are taken to imply work order. A parent task cannot be
started until all child tasks are completed. This paradigm is stronger
than inferences based on particular start or end dates assigned to
tasks, which in turns implies that GTG! is a planning tool in addition
to a GTD tool.

Removing subtasks would bring the GTG data model more in line with some
other GTD tools, but at the cost of making task order. It would become
significantly more difficult for GTG! to present the user with the task
(s)he *actually* should work on next, reducing its effectiveness as an
"external memory". Keeping subtasks, on the other hand, offers
opportunities for closer linking with not only Gantt-type planning
methods but others based on direction and dependency, including critical
path, event chains and PERT. Subtasks should therefore be retained.

### Task IDs

One obvious simplification is the removal the duplicate task IDs field.
GTG tasks stored in local files have both textual IDs (e.g. "12@1") and
random UUIDs (e.g. 21cb9d05-b609-452c-88fe-fac82bacccd4). Refer to [the
sample data file included with the GTG source
code](http://bazaar.launchpad.net/~gtg/gtg/trunk/annotate/head:/test/data/standard/xdg/data/gtg/866eace6-7482-41e9-b450-e9664a5d1602.xml)
for examples.

A second task ID field *might* be justified if it was very easily
human-readable *and* users were expected to regularly access or edit the
file. But neither is the case, so the removal of the ID field is
recommended.

In future situations (e.g. task export) where a user-readable task ID
field distinct from the title must be generated, this can be handled by
a backend.

## New fields — popular

Fields common to multiple other tools include:

- Creation/addition date-time
- Duration/length/work amount
- Percentage completion
- Priority

In order:

### Creation/addition date-time

The *creation/addition date-time* is an internal data store concept. In
GTG, it could be implemented as a per-task field, or via some separate
journalling mechanism (which might also be used to implement "undo"
functionality). The creation/addition of a task might not be displayed
to the user, but used to resolve ambiguities in synchronization between
tasks in multiple backends which cannot be resolved using any
combination of the other data fields. However, this sort of ambiguity
has not been encountered yet. For the moment, there is no compelling
reason to add a creation/addition date-time field.

### Duration/length/work amount

Two types of *duration/length/work amount* fields are visible in other
software. One type is simply a memo field which allows the user to
estimate, at any resolution, how much actual time will be required to
complete the task. This could be stored as text ("a while") or as a
date-time. The second type is in planning units, usually days, and
interpreted as "The number of days **worth of work time** to complete
this task, **given the amount of time I typicall spend on this type of
task in a day.**"

For example, a task "Paint the Mona Lisa" will take **10 hours** (yeah,
right!). If the user only spends 2 hours per day painting, then this
could also be expressed as **5 days** (worth of painting time). In
rigid, project-planning models like Gantt, this latter number can be
combined with the duration of other tasks ("Learn to paint as well as
Leonardo", etc.) to estimate the start & completion dates of future
tasks or the entire project.

A memo-type duration field may be useful in GTG, where it is prominently
displayed (for example, between the task title and the task body excerpt
in the Task Browser. This would allow the user to make better choices
between currently-available tasks, especially in the work view.

On the other hand a day-resolution duration field would not be useful if
it were optional (since the sum of durations of tasks, some of which
have no recorded durations, would be meaningless). If it were mandatory,
it would too rigidly impose a project-management paradigm on GTG! users,
which would likely conflict with their workflows. This type of duration
field is not recommended.

### Percentage completion

Percentage completion fields can be interpreted in relation to a
duration field; the user has thus far spent X% of the estimated duration
working on the task, but it is not complete. Or, they can be seen as
more abstract, implying quantity of work instead of quantity of time.
What this means will be different for every user.

The former case, the same objections as raised against a day-resolution
duration field apply. In the latter case, the use of "percentage"
falsely implies a much higher resolution than most people use to
consider individual tasks. Rhetorically, who will say that they have
done 75% of something instead of 70% of something? What would that
difference actually mean?

In lieu of a percentage completion field, the user should be
*encouraged* and *aided* in using subtasks to further break down any
task which they might partially complete. For example, entering "Make
sandwich ×8" might automatically create eight tasks named "Make sandwich
#1" through "Make sandwich #8".

### Priority

Priority simply means the relative importance of tasks. In GTG, this
concept would be useful in situations where:

- A parent task has multiple children, with start dates all passed,
- None of the children has an inherent dependency on any of the
  others; i.e. they could be executed in any order without difficulty,
  and
- The user is more anxious about one or more of the children.

Where the task body of the parent contains some length text with the
subtasks interspersed, that ordering may be significant or interpreted
as priority. However, when the parent and children are added through the
Task Browser without directly editing the parent body, subtask links in
the parent task body are added automatically and cannot be relied on to
imply any priority.

Interpreting certain children as higher-priority would allow presenting
them higher in the Work View for the user to select. Two means could be
used to do this:

1. Teaching the user the technique of exploiting alphabetization in the
   Work View, for example, prepending a "0" character to the title of a
   task which has higher-priority, or reordering child task links in a
   parent task body. Further, this could be supported by automatic
   assistance in the user interface.
2. Adding priority as an optional field in the data model, stored as a
   floating-point number between 0 (low) and 1 (high), else a null
   value. This must be supported in user interfaces signalling to the
   user that lets him/her distinguish where tasks are presented in a
   specific way because of their priority, or where they are
   unprioritized and the default ordering is used.

The latter method is recommended, as the corresponding user interface
changes will be much easier to implement.

## New fields — particular

Fields particular to other tools include...

### Postponement length/amount (RTM)

This field stores the amount of time a task's due date is extended
beyond the original. It forces the consideration of an *effective due
date,* which is the original date plus the postponement. Like the
creation/addition date, this is a journalling function, and not As
GAJ/Zeitgeist is implemented, the act of postponing a task could be
exported from GTG! as an event to be recorded, but there is no
compelling reason to add postponement tracking unless user demand
emerges.

### Other-person participation records (iCalendar)

This field (of which there may be more than one per task) stores contact
information relevant to other people who may be involved in such a task.
As suggested by the GTD synopsis (linked above), groups of participants
are only one of several possible *contexts* for grouping tasks. GTG!'s
tags can handle person-related contexts alongside other contexts without
the need for additional fields in the data model.

### Recurrence (iCalendar)

The iCalendar recurrence model uses a total of *four* fields to track
recurrence of VTODO items:

- recurid: unique ID for the recurring task set.
- exdate: a list of date-times for exceptions to a regularly recurring
  task.
- rdate: a list of date-times for irregularly recurring task.
- rrule: a grammar-based rule specifying recurrence of a task.

...the grammar for the rrule field is powerful but also complicated. It
allows for repetition every second, minute, day, week, month or year, on
any specific time or set of times within the repeat period, for a target
number of repetitions or until some fixed end date, with exceptions or
sets of exceptions specified using the same grammar. The specifications
alone for parsing these fields are ten pages of the RFC5545.

In part, this power in the specification is due to the fact that the
same fields are used to specify recurrence of calendar items. Some
tools, such as Google Calendar, have implemented interfaces for using
the full recurrence functionality for events, but do not provide the
same interfaces for the. This may indicate that such a powerful
recurrence model is not desired for tasks.

More fundamentally, the iCalendar model of recurrence uses the concept
of multiple instances of the same task/event. An instance may be
completed, but this does not necessarily mean that the task which is
recurring is complete. In GTG!, on the other hand, a completed task is
unambiguously completed. Adding iCalendar-style recurrence would change
this very basic concept in the GTG! data model.

Discussion around the desire for recurring tasks in GTG
(<https://bugs.launchpad.net/gtg/+bug/344432>) indicates some support
for implementing rules which parse task titles and create new ones when
the original is completed. This is similar to the special behaviour
described above in lieu of a priority field. Such behaviour would allow
the data model to remain simple, while presenting the user with optional
and possibly configurable options for creating batches of tasks to
capture recurring activity, so it is recommended.

### File attachments (iCalendar)

Tomboy and Gnote already allow users to link to files by entering
filesystem paths or <file://> URIs. These methods are recommended over
modifying the GTG data model to track attached files.

## Summary

The recommended changes to the GTG! data model are:

- **add** an optional priority field and memo-type duration field, and

- **remove** the ID field, keeping the UUID field only.

The above discussions contain numerous references to user-interface
enhancements which can be used to meet demand for certain functionality.
For such improvements, there may be a way to implement each one by
adding some field(s) to the task data model; but the GTG! developers
should prefer enhancements that **do not** alter the model. The only
exception is the possible addition of a *creation date-time*, as
discussed above. The forthcoming client/server separation using DBus
will allow better enforcement of this distinction.

