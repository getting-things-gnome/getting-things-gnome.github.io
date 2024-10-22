# Porting GTG to GTK3

## Environment

The development will take place on a linux box (ubuntu) to keep things
simple. You'll need to have installed virtualenv to start.

During this process, we'll be developping the package in a `virtualenv`
for simplicity's sake, and because it's part of current best practices.

If you want to do your development in `/path/to/dir`, try to get the
latest `virtualenv`, and run the following command:

    $ virtualenv --system-site-packages --distribute /path/to/dir

And activate it:

    $ cd /path/to/dir
    $ source bin/activate

This will activate your virtual environment (sandboxed environment), to
deactivate, just type deactivate in your terminal.

You'll need to install `pylint` to your `virtualenv` if it's not already on
your system, and you do intend to check and improve your code quality:

    $ pip install -U pylint

You'll need to install `sphinx` to your `virtualenv` if you intend to work
on documenting the package:

    $ pip install -U sphinx

You'll need to fetch the `liblarch` and `gtg` source code into a
subdirectory of `/path/to/dir`, or `/path/to/dir/src` to keep things tidy
and seperate the development code from the environment code.

## Workflow

The setup.py code has been modified to use distribute's `setuptools`
instead of `distutils` and `distribute` has been bundled with the code (as
it is recommended in the reference documentation for distribute). It
brings many advantages over the use of distutils, and adds quite some
commands too.

You can read more about it in the
[official distribute documentation](http://packages.python.org/distribute/)
or you could also explore the command line options:

    $ python setup.py --help
    # or for a list of commands that come with distribute
    $ python setup.py --help-commands

The main point of this being the ability to add the source packages to
the virtualenv's site-packages.

In order to install `liblarch`, run the following:

    $ python setup.py develop

instead of:

    $ python setup.py install

This way you can continue working in your source folder, testing your
changes, and running code without having to install anything.

Once you want to go back to your normal environment in the terminal,
you'll just have to deactivate the virtualenv with the following:

    $ deactivate

## Gtk3

liblarch has been ported manually using the migration tips in the
official reference. gtg was partially ported manually, until it became a
tedious and repetitive task after which we used the conversion script
referenced in the official migration reference, which broke non-gtk3
related code.

### Tips for manual renaming

More to come later.

`Gtk.Button("_Click here")`: In pygtk, it seems that when there is an
underline in the button label it indicates that the next character is a
mnemonic accelerator key (`Alt+C` in this case). In Gtk3 you can
accomplish the same by passing `use_underline=True` as an argument, i.e.
`gtk.Button("_Click here")` becomes
`Gtk.Button("_Press me", use_underline=True)`. For more information you
can [read more here](http://python-gtk-3-tutorial.readthedocs.org/en/latest/button_widgets.html#button).

### Renaming script improvements

More to come later.

### D-BUS

### Gnome keyring

The gnomekeyring is a static binding which depends on gtk2, which means
in gtk3 we won't be able to use this. This is a good opportunity to port
gtg to using the secret service api over d-bus.

### libpeas

A plugin system for gtk3 apps.

## Strings cleanup & python3

Porting to python3 was not the main goal, and still is not the main goal
of this porting effort. However the code include certain unnecessary
string concatenations which are less efficient then string formatting.
In the process since these string concatenations were replaced by their
string formatting equivalent.

Since there is a wide support in pre-python3 interpreters for python3
style string formatting, and printing, those were changed as well, which
should simplify any future effort in porting to python3.

## Interesting links

- [The official guide used](https://live.gnome.org/PyGObject/IntrospectionPorting)
- [Sugarlabs porting notes](http://wiki.sugarlabs.org/go/Features/GTK3/Porting)
- [Sugarlabs Gtk3 development notes](http://wiki.sugarlabs.org/go/Features/GTK3/Development)
- [Experiences of porting an app into GTK3](http://www.jeremyscheff.com/2012/02/some-notes-on-porting-from-pygtk-to-pygobject/)
- [Python/Gtk3 Tutorial, Tree and List Widgets section](http://python-gtk-3-tutorial.readthedocs.org/en/latest/treeview.html)
