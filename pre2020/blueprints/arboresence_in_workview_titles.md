# Show Arborescence In Workview Titles

## Use case

My task is to set up a Computer for someone. Here is how the task breaks
down, as it would be shown in the default view:

1. Setup Sylvie's PC
   1. BIOS
   2. System
      1.  OS
      2.  Drivers
   3. Software
      1. OpenOffice
         1. Install
         2. Configure
      2. Firefox
         1. Install
         2. Configure

Here is how it shows up in Workview Mode:

- Bios
- OS
- Drivers
- Install
- Configure
- Install
- Configure

My problem is that I can't figure out which software I have to install
or configure when I'm in Workview Mode. I need more info about the
task's context.

## Proposal

My proposal is to add an option which diplays the subtask's Arborescence
in its title, with an emphasis on the subtask's name. Here is how it
would show :

- Setup Sylvie's PC/**BIOS**
- Setup Sylvie's PC/System/**OS**
- Setup Sylvie's PC/System/**Drivers**
- Setup Sylvie's PC/Software/OpenOffice/**Install**
- Setup Sylvie's PC/Software/OpenOffice/**Configure**
- Setup Sylvie's PC/Software/Firefox/**Install**
- Setup Sylvie's PC/Software/Firefox/**Configure**

This way, I can see which task I can do right now without ignoring its
context.

Answer from [LionelDricot](https://wiki.gnome.org/LionelDricot):

This proposal cannot be accepted because, in your example, GTG is not
used as a list of tasks but like a file system. I've explained this in
[the mailing list](https://lists.launchpad.net/gtg-contributors/msg00769.html). We
are in the process of redesigning GTG to make that clear. You may be
interested by reading our
[Manifesto](../../manifesto).

