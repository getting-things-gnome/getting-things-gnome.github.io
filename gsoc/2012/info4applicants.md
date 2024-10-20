# GSoC2012: information for the GTG applicants

This year, several ideas have again been proposed to apply for a GSoC
with GNOME and Getting Things GNOME! Those ideas are posted here:
[SummerOfCode2012/Ideas/](https://wiki.gnome.org/Outreach/SummerOfCode2012/Ideas/).

As you can see on this page three ideas are suggested:

- Design a new UI for GTG that will fit in the Gnome 3.x desktop
- Task editor rework
- Reoccurring tasks

(We're of course open to other propositions! It would be wise to contact
the developers beforehand, though.)

This page summarizes some information for the candidates that would be
interested in working on those project, and help them for their
application.

## Picking a bug to solve to fill the application

As written in [SummerOfCode2012/Students](https://wiki.gnome.org/Outreach/SummerOfCode2012/Students),
the applicants should pick a bug related to the module for which they
want to contribute in their project. This allows them to start the
collaboration with the project, to work with the project's development
tools and to see what the development process is in this project (as
well as getting in touch with the developers). The aim is to demonstrate
your willingness and capacity to work on the module targeted by the
project proposal. The bug you pick shouldn'ttherefore necessary be
difficult ones, but relevant. Choose carefully.

In order to help you to pick a bug, you will find some advices and small
lists below for each project.

### Design a new UI for GTG that will fit in the Gnome 3.x desktop

Please contact [BertrandRousseau](https://wiki.gnome.org/BertrandRousseau) if you need
guidance for this.

For this project, someone would design and propose an improved UI for
GTG that respect the new Gnome 3 HIG. However, apart from the generic
bugs directly related to the GSoC idea (see below), most existing bugs
don't involve UI design or GTK3 port. Since this project will require to
code using python GTK3, it would be most useful to work with those
widgets and python bindings as soon as possible.

To apply to this project, I would thus advise any applicant to start
coding a small & simple prototype of a task browser using python GTK3.
This should demonstrate some basic user interaction related to the task
browser: e.g. display a window which list several tasks. It could very
well reproduce the existing UI, but it should use python GTK3. **Note:
this could very well be a non-working prototype, which would only
display hardcoded infromation (indeed, getting everything to work from
the start will probably be non-trivial), but it MUST show that you can
work with UIs**. Once it runs, the applicants should notify his/her work
in the bug report(s), register his/her personal branch in launchpad (bug
and repository lists), and ask a developer to review the code (for code
style, etc) using launchpad or the mailing-lists. This work will
bootstrap the branch he/she will work on during the GSoC, should the
project be accepted.

If you however prefer to work on a less generic bug, this is also
possible. Pick a bug from launchpad related to UI and try to fix it
(perform the same actions as mentioned below). You can pick a bug from
the list below for instance.

GTK3/GNOME3-related bugs:

- GTG needs a UI redesign: <https://bugs.launchpad.net/gtg/+bug/885320>
- GTG needs a GTK3 port <https://bugs.launchpad.net/gtg/+bug/897136>

UI-related bugs (the first ones are easier):

- workview icon is wrong <https://bugs.launchpad.net/gtg/+bug/825774>
- Tags' background color should be the tag's color <https://bugs.launchpad.net/gtg/+bug/339855>
- New field: effort <https://bugs.launchpad.net/gtg/+bug/615032>
- Automatic generation of tag color: <https://bugs.launchpad.net/gtg/+bug/644993>
- Create a tag editor <https://bugs.launchpad.net/gtg/+bug/643522>
- Color picker/icon chooser for tags: <https://bugs.launchpad.net/gtg/+bug/320264>
- Add more information about which tasks are listed in the browser: <https://bugs.launchpad.net/gtg/+bug/844963>
- Implement a task detail pane to show in the main taskbrowser window: <https://bugs.launchpad.net/gtg/+bug/341871>

### Repeating tasks

Please contact [LionelDricot](https://wiki.gnome.org/LionelDricot) if you need guidance for
those.

Some related bugs:

- <https://bugs.launchpad.net/gtg/+bug/734622>
- <https://bugs.launchpad.net/gtg/+bug/692555>
- <https://bugs.launchpad.net/gtg/+bug/344432>
- [Discussion on user mailing list](https://lists.launchpad.net/gtg-user/msg00389.html)

### Text editor rework

Please contact [LionelDricot](https://wiki.gnome.org/LionelDricot) if you need guidance for
those.

- [blueprint for text editor rework](../../pre2020/blueprints/taskeditor_rework)

