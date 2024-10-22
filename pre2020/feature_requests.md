# Existing feature requests for GTG

This list was compiled by Izidor on August 16, 2011 by [bugs for
GTG](https://bugs.launchpad.net/gtg). The list was updated on February
12, 2012. Feature requests and bugs are in no particular order.

## Rewrite GTG into PyGI (GTK3)

## Show parents for tasks in workview

- <https://bugs.launchpad.net/gtg/+bug/607586>
- <https://bugs.launchpad.net/gtg/+bug/316922>

## Repeating tasks

- <https://bugs.launchpad.net/gtg/+bug/734622>
- <https://bugs.launchpad.net/gtg/+bug/692555>
- <https://bugs.launchpad.net/gtg/+bug/344432>

## Ideas for backends

- [Google Tasks Backend](https://bugs.launchpad.net/gtg/+bug/788564)
- [TeamBox](https://bugs.launchpad.net/gtg/+bug/667311)
- [ProjectPier](https://bugs.launchpad.net/gtg/+bug/667310)
- [Producteev](https://bugs.launchpad.net/gtg/+bug/634978)
- [Tracker](https://bugs.launchpad.net/gtg/+bug/508521)
- [Directory/File system](https://bugs.launchpad.net/gtg/+bug/625025)
- [Bazaar](https://bugs.launchpad.net/gtg/+bug/582558)
- [Google Calendar](https://bugs.launchpad.net/gtg/+bug/613382)
- [toodledo](https://bugs.launchpad.net/gtg/+bug/519137)
- [Basecamp](https://bugs.launchpad.net/gtg/+bug/514089)
- [Hiveminder](https://bugs.launchpad.net/gtg/+bug/513577)
- [Todoist](https://bugs.launchpad.net/gtg/+bug/539024)
- [iCal XML](https://bugs.launchpad.net/gtg/+bug/336612)
- [GetOnTracks](https://bugs.launchpad.net/gtg/+bug/339264)
- [Bugzilla](https://bugs.launchpad.net/gtg/+bug/494967)
- [ZeitGeist](https://bugs.launchpad.net/gtg/+bug/530582)
- [Github Issues](https://bugs.launchpad.net/gtg/+bug/935979)
- [RSS/Atom import backend](https://bugs.launchpad.net/gtg/+bug/935981)
- [Mail (IMAP/POP) backend](https://bugs.launchpad.net/gtg/+bug/935983)

How to choose which backends are officially supported? Which not?

## Hamster plugin bugs/feature requests

- <https://bugs.launchpad.net/gtg/+bugs?field.tag=hamster>

## D-Bus interface

- really separate server an GUI of GTG using D-Bus

## Text editor rework

Look [there](pre2020/blueprints/taskeditor_rework).

## UI improvements

- <https://bugs.launchpad.net/gtg/+bug/644993>
- <https://bugs.launchpad.net/gtg/+bug/339855>
- <https://bugs.launchpad.net/gtg/+bug/415803>
- <https://bugs.launchpad.net/gtg/+bug/341871>
- <https://bugs.launchpad.net/gtg/+bug/643522>

## Gantt diagram plugin

- <https://bugs.launchpad.net/gtg/+bug/495475>

## New representation of tasks

- <https://bugs.launchpad.net/gtg/+bug/340022>

## Multiple selection of tags

- Decide wheter we want to have INTERSECTION or UNION of tags.
- <https://bugs.launchpad.net/gtg/+bug/522971>

## Nifty Drag and Drop support

- DnD from Mozilla Thunderbird
  - Task Coach implementation → requires e-mail password and then
    fetch it manually, the password is lost after restart
  - an extension for Thunderbird to convert this e-mail into GTG task
- Postler – it uses our D-Bus interface for converting e-mail into a
  task, bugs with special characters like : „ # etc.
- DnD a snippet of text into GTG window → create a new task with that
  text
  - special support for links – I want to look at this page later
- DnD between tags and tasks:
  - task on tag, tag on task => task gets a new tag
  - task on "Tasks without tags" or vice versa => tasks is removed
    all its tags

Bugs:

- <https://bugs.launchpad.net/gtg/+bug/500727>
- <https://bugs.launchpad.net/gtg/+bug/512228>
- <https://bugs.launchpad.net/gtg/+bug/504874>
- <https://bugs.launchpad.net/gtg/+bug/783831>
- <https://bugs.launchpad.net/gtg/+bug/780113>

## Permanent tags

When there is no longer active tasks associated to a tag, it disappear
and it is very annoying to have to re-create same tags several times
over a long time of use.

It would be great to put an option which enable a persistent mode for
tags.

There must be option to use default behavior in 0.2.4 => hide them

I think we will need to have remove option in right click menu

in case of removing => we dont need reset tag menu item

- <https://bugs.launchpad.net/gtg/+bug/499320>

## Official GTG server, assigning tasks to people through XMPP backend

- <https://bugs.launchpad.net/gtg/+bug/681487>
- <https://bugs.launchpad.net/gtg/+bug/614523>
- <https://bugs.launchpad.net/gtg/+bug/540164>
- <https://bugs.launchpad.net/gtg/+bug/339324>

## Quick add toolbar

- <https://bugs.launchpad.net/gtg/+bug/352686>
- <https://bugs.launchpad.net/gtg/+bug/352637>
- <https://bugs.launchpad.net/gtg/+bug/671245>

## Notification area

- <https://bugs.launchpad.net/gtg/+bug/591920>
- <https://bugs.launchpad.net/gtg/+bug/620752>

## Reordering tasks

- use a **weight** attribute for sorting to allow reordering
- <https://bugs.launchpad.net/gtg/+bug/497164>
- <https://bugs.launchpad.net/gtg/+bug/400267>
- <https://bugs.launchpad.net/gtg/+bug/553910>
- <https://bugs.launchpad.net/gtg/+bug/811702>
- <https://bugs.launchpad.net/gtg/+bug/516392>
- <https://bugs.launchpad.net/gtg/+bug/345575>
- <https://bugs.launchpad.net/gtg/+bug/321905>

