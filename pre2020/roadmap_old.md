# Roadmap

*Maps?! Where we’re going, we don’t need maps!*

... but maybe we actually do! As the number of GTG contributors is
growing, it has become increasingly interesting to lay out some plans
about how we should arrange the development of GTG in time. This page is
an attempt at proposing such a plan. Feel free to discuss some point, in
this page or preferably through our mailing-lists and IRC chan (#gtg on
GimpNet).

## This page needs updating

This needs to be rewritten in 2020. 0.3.1 has been released long ago,
0.4 is the upcoming GTK3+Python3 release. See
<https://github.com/getting-things-gnome/gtg/milestones/> in the
meantime.

## Getting Things GNOME 0.3.1

Getting Things GNOME 0.3.1 should be done in really short time and its
only change should be porting GTG to GTK3. Most of the time, it should
be only about refactorization code. We have some bugs which could be
solved only by porting to GTK3, e.g. Evolution synchronization.

This milestone will mainly focus on technical aspects, not on new
features.

- Clean up the bug database, perform a serious triage job in our bugs.
- Port to GTK3
- Port to Python3
- Make the whole code base PEP8/Pylint compatible
- Put together a good/useful test suite
- OPTIONAL: improve and integrate the export plugin in core

## Not so far future

- sort things out about plugin maintainance issues
- improve translations quality/completeness -- find help within GNOME
- split GTG into a daemon and client
- [redesign to match GNOME 3](design)
- [Reworked synchronization services](blueprints/backends) --
  easy to write Hello World synchronization services, extract
  synchronization code into GTG toolkit, read only tasks
- [Filtering by mutliple tags](blueprints/filtering_by_multiple_tags)
- [task editor rework](blueprints/taskeditor_rework)
- [desktop integration](blueprints/desktop_integration)
- implementing many synchronization services (there are many requests
  in the bug tracker)
- [recurring tasks](blueprints/repeated_tasks)
- priority by drag'n'drop of tasks, better sorting

## Far future

- [statistics](blueprints/statistics)
- GTG web client
- Android app
- \<insert your wishes here>

# Past Versions

## Getting Things GNOME 0.3

Getting Things GNOME 0.3 is the next major version of GTG. Its main
objective is to bring stability to released GTG 0.2.9:

- reasonable performance
- perfectly working synchronization services: Google Tasks, Remember
  the Milk, Launchpad, Tomboy/Gnote, Twitter, Identica, MantisBT
- improve export plugin (see its bugs)
- better packaging of plugins and synchronization services every
  distribution resolves dependences itself

