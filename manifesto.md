# Manifesto

## What is GTG?

Getting Things GNOME! (GTG) is a personal tasks and TODO-list items
organizer for the GNOME desktop environment inspired by the Getting
Things Done (GTD) methodology. GTG is designed with flexibility,
adaptability, and ease of use in mind so it can be used as more than
just GTD software.

GTG is intended to help you track everything you need to do and need to
know, from small tasks to large projects.

## About this document

This document's purpose is to help all GTG contributors to collaborate
efficiently. It tries to provide clear definitions of the project's
objectives and its most important concepts. It acts therefore as a
founding document for the project. Every initiate taken by a member of
the GTG community is thus expected to be in agreement with this
manifesto.

The content of this manifesto is open to comments and critics. It will
be maintained and revised when needed to take into account the outcome
of every relevant discussions happening in the community. It can thus be
considered at all time as a reference document.

## GTG goals

GTG's primary goals are:

1. **Relieve stress**

   GTG tries to relieve stress by taking care of everything, it
   makes sure you never forget anything and you never miss a
   deadline.

2. **Focus on what's relevant**

   GTG helps you to focus on the most relevant tasks depending on
   your time, place and deadlines.

3. **Make real progress**

   GTG helps you to know why you need to perform a task so that you
   can make sure that you really progress towards your goals.

4. **Avoid procrastination**

   GTG encourages you to do what needs to be done.

Those goals are listed by order of importance. Every single design
decision in GTG should relate to those goals.

### What GTG is / What GTG is not

- **GTG is not a simple todo-list application**: it is not made to
  just handle a bunch of simple lists (groceries, etc.). It is
  therefore not minimalistic. GTG is a personal task manager: it is a
  tool that allows people to identify and track down everything they
  have to do and help them to organize themselves. So, contrary to
  simple todo list tools, GTG allow to implement an *personal
  organization system* (like GTD, for instance).

- **GTG is not a Getting Things Done tool**: GTG doesn't implement a
  specific organization process. However, GTG wants to allow people to
  build their personal task management process (like: 1. receive
  task, 2. sort out tasks, 3. identify what to do, 4. do, 5. review).
  It is our view that nobody quite exactly follow the policy behind a
  specific organizational system completely, so why bother imposing
  it? We want the user to be able to build his/her own process so that
  it fits his/her life and needs.

- **GTG wants to be simple, yet powerful**: Our model is gedit: at its
  core, it appears as a clean and basic text editor, but when you
  start to use it, you can customize it quite a lot, so that in the
  end not 2 people exactly use the same way. We want GTG to feel the
  same: at its base, you use it to store and organize your tasks, with
  a very limited number of available mechanisms/features, but it could
  become much more personal and powerful as you enable additional
  features (plugins, etc.) and configure it. That means GTG should
  have a simple/basic core that allows someone to organize himself,
  and "extension paths" that allows to customize and empower the
  experience.

- **GTG is made for the GNOME desktop**: It should integrate
  seamlessly in it. It should be able to 'play ball' with other GNOME
  technologies, and freedesktop.org technologies. It should respect
  the GNOME HIG too.

- **GTG should be "socially aware"**: In the future, we plan to
  include collaborative task management in GTG.

### Tasks

A task is an action you or someone else can do to change the current
situation into another situation.

A task description always starts with a verb. When reading a task
description, one should immediately understand what do to to accomplish
that task. It is also important that it should be clear to decide if a
task has been accomplished or not.

A task has only two authorized relations to its owner: "I need to do it"
or "I don't need to do anything about it", without any intermediate
point. By default, tasks are in the "I need to do it" relation. This
changes in two situations:

- The task has been accomplished by you -> task is "I don't need to do
  anything about it" (marked as Done)

- You don't need to accomplish the task for whatever reason -> task is
  "I don't need to do anything about it" (marked as Dismissed)

### Goal

A goal is a specific situation targeted by someone which results of the
accomplishment of at least one task. To be useful, a goal should have an
observable outcome: you should be able to know precisely when you reach
the goal. "Becoming rich" is not a good goal. "Having 1,000,000$ on my
saving account" is a good goal because it is observable.

Goals are also tasks. In order to be good goal, it should also starts
with a verb (which is often more generic, like "having" or "being").

A goal is also very often a task that lead to something else see
comment. Why having 1,000,000$? For the sake of it? Because you want to
be an early retired? So the goal should be "being an early retired". Why
do you want that after all? To have the time to write a book? Thus, the
goal should probably "Write a book". In that case, writing the task
"Write a book" will save you the hassle of earning 1,000,000$!

It should be underlined that a goal could be shared by multiple person.
Working collaboratively towards a goal is a "project".

### Everything is a task

In life, everything is a task. Even the biggest project is only a simple
list of tasks. As we said, most goals are also tasks. GTG's vision is
that everything is a task.

In order to achieve a task, you may need to achieve some other tasks
first.

## Implementation directives

This section provides additional considerations that must be taken into
account when implementing something in GTG. Its purpose is to provide
directives to contributors to help them know how GTG's primary goal can
be reached.

### Relieve Stress

- Ensure that entering a new task is dead-easy. A user should be able
  to enter a new task without having to think about the task creation
  process.
- Whenever possible, directly identify the sources of the new task and
  connect them to GTG: e-mails, webpages, etc.
- Enable access to your tasks and collect new tasks from anywhere
- Enable other people who share a goal with you to assign you some
  tasks

### Focus On What's Important

- Offer a short list of tasks that are actionable without the noise of
  all the context.
- Highlight tasks due soon or already overdue.
- Make it easy to create a dependancy between a task (in order to not
  list irrelevant tasks in the workview).
- Allow to display only tasks related to a specific context.

### Make Real Progress

- Make it easy to create a dependancy between two tasks.
- Make it easy to refine a task in several subtasks.
- Allow users to link tasks to a goal and warn when a goal has no
  task.
- Track progress made towards the goals.

### Avoid Procrastination

- Maintain all information related to a task in a single place.
- Encourage the use of an action verb in the title of a task.
- Encourage the user by keeping track of what has been done.
- Allow to assign a task to another person to share the workload.

------------------------------------------------------------------------

# On-going discussions about the text

**Collaborative work**

[BertrandRousseau]: https://wiki.gnome.org/BertrandRousseau
[LionelDricot]: https://wiki.gnome.org/LionelDricot

[BertrandRousseau][BertrandRousseau], 2012/03/26 - 01:22

By the end of the document, there some direct or indirect mention to a
collaborative use of GTG. These aspects should be better defined.

**Who's the public?**

[BertrandRousseau][BertrandRousseau]: IMHO, it's GTG's community of
contributors. Not users, I don't think they care directly about the
GTG's goals, they just use the *product* of it.

**"Never miss deadlines"**

[BertrandRousseau][BertrandRousseau]:\_ I think ensuring that you never
miss a deadline is actually a requirement of the first goal: lowering
stress by making sure you don't miss anything. GTG gives this guarantee.
So, I moved it there. However, I still kept a reference to deadline in
goal #2.

**"Narrow focus"**

[BertrandRousseau][BertrandRousseau]: "narrow focus" is not a goal. I
suggest: **Focus on what's relevant**.

[LionelDricot][LionelDricot]: good suggestion

**"Wide focus"**

[BertrandRousseau][BertrandRousseau]: Same comment as for 'narrow
focus'. I suggest: **Real progress**.

[LionelDricot][LionelDricot]: I like it the suggestion. Another idea
would be to take the concept of altitude seen in the GTD book.

**Form**

[BertrandRousseau][BertrandRousseau]:

The document should probably more formal. The text could alternate
between a first part where things are first defined formally, then a
second part where things are then explained more informally.

Ex:

- A task can only accept two types of relation to the user's
  objectives: it is either **required** to progress towards these
  objectives, or **not required**. Moreover, when a task is **not
  required**, it can only be for two reasons: the user either
  performed the task, or it has been made irrelevant.

Indeed, when a user creates a task, he/she is supposed to accomplish it.
There could only be two situation for which the task is no longer to be
made: it has been done, or it has became irrelevant. The latter is the
case when a situation has changed due to the intervention of something
external to the user (e.g. "Buy groceries" when your significant other
already did it).

**"A goal is also very often a task that lead to something else"**

[BertrandRousseau][BertrandRousseau]:

This is a tautology: this is the very definition that's been given to a
task earlier.

**What is GTG?**

[BertrandRousseau][BertrandRousseau], 2012/04/22 - 12:47

Added this section to improve the definition of GTG, the view behind the
project. It comes from a discussion with A. Day, Alex B., etc.

