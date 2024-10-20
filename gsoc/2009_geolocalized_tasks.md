# Geolocalized-tasks plugin

## Prerequisites

- [libchamplain](http://projects.gnome.org/libchamplain/) :
  Libchamplain is a C library providing a
  [ClutterActor](/ClutterActor) to display maps. It also provides a
  Gtk+ widget to display maps in Gtk+ applications. Mono, Python and
  Perl bindings are available.
  - You can download libchamplain from:
    - There are no current python bindings for cluter 1.0, the
      last version is 0.9 so for the geolocalized-tasks plugin to
      work you will need [libchamplain version
      0.3.5](http://download.gnome.org/sources/libchamplain/0.3/libchamplain-0.3.5.tar.gz)
      that you can get
      [here](http://download.gnome.org/sources/libchamplain/0.3/libchamplain-0.3.5.tar.gz).
      You also need to have all the clutter 0.8 development
      libraries installed.
    - Once python-clutter reaches version 1.0 you can use the
      current development version. You can get it from
      [git://git.gnome.org/libchamplain](/git%3A//git.gnome.org/libchamplain)
      (*git clone git://git.gnome.org/libchamplain*)
    - libchamplain is now available in the ubuntu karmic package
      repository, but I haven't been able to test it yet so I
      don't know how it works out.
  - To compile from the source do the following commands:
    - *./autogen.sh --prefix=/usr --enable-python*
    - *make*
    - *sudo make install* (you need to make install as root)

The package python-clutter-gtk-dev and libgconf2-dev are required in
order to compile libchamplain. On Ubuntu Karmic, you can install the
former from the [Following ppa](https://edge.launchpad.net/~francesco-marella/+archive/ppa)

- [Geoclue](http://www.freedesktop.org/wiki/Software/GeoClue) :
  Geoclue is a modular geoinformation service built on top of the
  D-Bus messaging system. The goal of the Geoclue project is to make
  creating location-aware applications as simple as possible.
  - You can download Geoclue from:
    - [git://anongit.freedesktop.org/git/geoclue](/git%3A//anongit.freedesktop.org/git/geoclue)
      (*git clone git://anongit.freedesktop.org/git/geoclue*)
    - The latest release is available here:
      <http://folks.o-hand.com/jku/geoclue-releases>.
    - Geoclue is also available in the ubuntu karmic package
      repository, like libchamplain I haven't tested these
      packages in karmic but I saw you have to install the wanted
      providers (each provider has a package).
  - To compile from the source do the following commands:
    - *./autogen.sh --prefix=/usr*
    - *make*
    - *sudo make install* (you need to make install as root)
- python-geoclue: Python Geoclue module. python-geoclue
  is nice API interface for Geoclue, based on Geoclue's D-Bus API.
  - This module depends on Geoclue and should be the only thing you
    need but to make sure you have all the needed dependencies I'll
    leave Geoclue in the list.
  - You can download python-geoclue from:
    - Deb package: deb package link (2024: link not working)
    - Source: <http://live.gnome.org/gtg/soc/python_geoclue>
  - To install the module from the source do the following:
    - *sudo ./setup.py install* (you need to run setup as root)

## Where you can get it!

You can download GTG with the geolocalized-task's plugin from:

- [Getting Things Gnome's current development branch](https://code.launchpad.net/~gtg/gtg/trunk)
  - I will add a direct link to a package containing only the plugin
    soon.
  - The plugin is shipped with GTG but currently the latest GTG
    release is 0.1.2 and the plugin was only made prior to this
    release.

## How to install the plugin

This plugin is shipped with Getting Things Gnome's latest version.

Anyway, if you want to install the plugin you just have to place it in
the following directory:

- $XDG_HOME/gtg/plugins/
  - $XDG_HOME is normally your $HOME/.config directory

## How to use it

The plugin is easy to use but you should have one thing in mind, once
enabled it extends the **Work View** to tasks you can do "right now and
**right here**".  
The location is a tag attribute and when a tag is associated with a
task, the task gains the tag's location. If two different tags are
associated with a task and both have the location set, the task will
gain those two location and will be displayed in the map with those two
locations.

You can associate a location to a task mostly in two distinct ways:

- In the tag view, if you right click on the desired tag you can
  choose "Assign a location to this tag" and in the dialog that opens
  you can pin point the location in the map, assigning that location
  to the tag. At any time you can change the tag's location by doing
  the same.
  - ![assign_location_to_tag.png](http://www.paulocabido.com/soc/assign_location_to_tag.png)
  - ![dialog_assign_location_to_tag.png](http://www.paulocabido.com/soc/dialog_assign_location_to_tag.png)
- You can also add the task's location while adding ou modifying a
  task. In the task editor there is a button named "Set/View Location"
  that will open a dialog in witch you can set the location if no
  location is set or view the task's location.
  - ![task_editor_set_view_location.png](http://paulocabido.com/soc/task_editor_set_view_location.png)
  - If no location is defined you'll get a dialog like this one
    (below) where you can associate the location to a new tag or to
    a existing tag (if any tag without a location is associated with
    the task). I don't know if this is the best option for the UI,
    if you have any suggestion to change this dialog, let me know.
    - ![set_location.png](http://paulocabido.com/soc/set_location.png)
  - If the location is already set, you will get a dialog like this
    one:
    - ![view_location.png](http://paulocabido.com/soc/view_location.png)
- There is also a preferences dialog where you can set the plugin's
  settings. It's currently listed under the Plugins menu but soon it
  will be available in a a configuration option in the plugin manager.
  In the settings dialog you can change:
  - The location determination method. This is how your location
    will be discovered by Geoclue, witch resources to use. The
    network resource should always be left enabled, it works very
    well and is a good backup when one of the others fails to
    acquire the current position.
    - If a provider is installed but isn't available it will not
      show up as active in the settings. For example, if you have
      the gpsd provider installed but don't have a gps configured
      it will not be shown as active.
  - The proximity factor. Because users may want tasks within a
    radius of, for example, 5km (10km, 15km, etc) to be shown I
    created this setting to be adjustable. The distance is measured
    in kilometers.
    - ![settings.png](http://paulocabido.com/soc/settings.png)

