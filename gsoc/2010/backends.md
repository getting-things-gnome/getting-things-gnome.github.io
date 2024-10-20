# Getting Things GNOME! online integration proposal

[Getting Things GNOME!](https://edge.launchpad.net/gtg) (GTG) is an
organizer for the GNOME desktop environment, focusing on usability and
ease of use.

## What we're planning to do

The "next big thing" planned for GTG is a seamless integration with
online services (see our [roadmap](../../roadmap)).

Let me explain what we are trying to achieve with an example:

Ed is a busy contractor during the day, FLOSS developer during the
night. He obviously has a lot of things in its TODO list, but it's hard
to keep such list always handy \*and\* organized. He keeps some of his
tasks on his cell phone, on a commercial free application such as
[remember the milk](http://www.rememberthemilk.com) or
[toodledo](http://www.toodledo.com/). His wife sends him emails about
what he has to buy on his way home. He also has bug to fix in his floss
project, listed on Launchpad. How can Ed keep up with that?

The answer is GTG! (I suppose you saw that coming). GTG will store and
get tasks from multiple sources in a unified way.

- Using tags, it will keep task context separate. All the tasks coming
  from Ed's Launchpad will be tagged @FLOSS (or whatever Ed prefers),
  and his wife emails containing TODO in the subject will be
  tagged @personal.

This feature is getting GTG users pretty excited, as we've already
thought/had requests for support of many services. Here a short list:

- Desktop CouchDb
- Launchpad
- Bugzilla
- twitter/identica (import only, tweets/dents tagged as #todo)
- tracker
- google docs (export only)
- toodledo
- the ical format
- google tasks (when the api will come)
- the xml format
- plain text (wiki?), optionally under bazaar/git control
- a directory tree

We already have plugins for:

- Evolution
- remember the milk
- JSON Those should be ported to the common GTG framework and expanded
  as needed.

Further analysis of the backends framework can be found:

- [on GTG mailing list](https://lists.launchpad.net/gtg/msg00660.html)
- [on launchpad](https://bugs.edge.launchpad.net/gtg/+bugs?field.tag=backends)

## What we'd like to have done during GSoC

The student should write the common framework to handle synchronization
and the user interface.

Moreover, the student should write support for several services (as many
as possible) and the documentation on how to make one.

Those three plugins should be ported as well.

A special effort will be needed to handle errors and timeouts.

