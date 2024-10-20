# Getting things GNOME! integration with online services

## Project context

[Luca Invernizzi](http://allievi.sssup.it/invernizzi)'s project for the
[Google Summer of Code](http://socghop.appspot.com/), 2010 edition.

## Abstract

Development of a framework to synchronize the TO-DO manager "Getting
Things GNOME!" with online (and offline) providers of "things to do".
Providers can range from traditional online TO-DO managers à la Remember
the Milk to bugs assigned to you in a bug tracker. A few of them will be
implemented: Remember the Milk, Evolution Data Server, Launchpad ,
twitter (for adding tasks when receiving direct messages marked #todo).

## Proposal

An extended explanation of what is planned is available [here](2010_invernizzi).

## State of the project at the end of GSoC

- Support for multiple backends in GTG core and update of the
  local-file backend ([state of the merge](https://code.edge.launchpad.net/~gtg-user/gtg/backends-main/+merge/32583))
- UI for adding/removing/editing backends ([state of the merge](https://code.edge.launchpad.net/~gtg-user/gtg/backends-window/+merge/32005))
- Support for gtg:// URI in gnome ([state of the merge](https://code.edge.launchpad.net/~gtg-user/gtg/uri-support/+merge/32128))
- Utilities to create complex backends ([state of the merge](https://code.edge.launchpad.net/~gtg-user/gtg/backends-utils/+merge/32278))
- Support for TODO items in Gnome-Activity-Journal ([state of the merge](https://code.edge.launchpad.net/~invernizzi/gnome-activity-journal/GAJ-todo-gtg/+merge/28799))
- Zeitgeist backend (export)
- Remember the milk backend (two way)
- Evolution Tasks backend (two way)
- Evolution Mails backend (import)
- Tomboy/gnote backend (two way, [state of the merge](https://code.edge.launchpad.net/~gtg-user/gtg/tomboy-backend/+merge/32641))
- Twitter backend (import only)
- Identi.ca backend (import only)
- Couchdb backend (two way)
- Lauchpad backend (import only)

The core parts of this projects will be released in GTG 0.3 version,
coming in the fall of 2010. Most of the backends should be included,
too.

## Blog posts

- [overview](http://allievi.sssup.it/techblog/?p=246)
- [weekly report 0](http://allievi.sssup.it/techblog/?p=307)
- [weekly report 1](http://allievi.sssup.it/techblog/?p=323)
- [weekly report 2](http://allievi.sssup.it/techblog/?p=352)
- [weekly report 3](http://allievi.sssup.it/techblog/?p=368)
- [weekly report 4](http://allievi.sssup.it/techblog/?p=393)
- [weekly report 5](http://allievi.sssup.it/techblog/?p=412)
- [weekly report 6](http://allievi.sssup.it/techblog/?p=427)
- [weekly report 7](http://allievi.sssup.it/techblog/?p=465)
- [weekly report 8](http://allievi.sssup.it/techblog/?p=483)
- [weekly report 9](http://allievi.sssup.it/techblog/?p=517)
- [weekly report 10](http://allievi.sssup.it/techblog/?p=527)
- [weekly report 11](http://allievi.sssup.it/techblog/?p=542)
- [weekly report 12](https://lists.launchpad.net/gtg-gsoc/msg00078.html)

### Where to find the code

I'm pushing my work on a
[branch](https://code.edge.launchpad.net/~gtg-user/gtg/multi-backends__invernizzi_gsoc)
on Launchpad. Before testing, backup you gtg directory:

-   

        tar czf gtg.tgz .local/share/gtg
        tar czf gtg_conf.tgz .config/gtg

To test it, execute:

-   

        bzr branch lp:~gtg-user/gtg/multi-backends__invernizzi_gsoc gtg-invernizzi
        cd gtg-invernizzi
        ./scripts/debug.sh

## More Information

- Use this [mailing list](https://edge.launchpad.net/~gtg-user) if you
  want to ask something about this.

