# Mockups

## The plug-in framework.

- The plug-in framework is divided into three parts:
  - The Plug-in Manager that handles the GUI for the plug-ins. In
    the plug-in manager the users can see the available plug-ins,
    their description and enable/disable plug-ins.
    - [Plug-in Manager GUI (Image)](http://paulocabido.com/soc/mockups/plugin_manager_gui.png)
  - The Plug-in Engine. This part handles the plug-in load,
    activation and deactivation, etc.
  - The Plug-in API. This part of the framework consists on a group
    of allowed methods for the plug-ins to use.

## Add the Geolocalized tasks as a plugin.

- The plugin implements a new option for a user to define the task's
  location. This option is situated on the right sidebar under the
  task dates.
  - Possible ways to do this:
    - A new window opens and the user defines all the options
      there.
    - The localization options are included on the Add task
      interface. A new pane that can be hidden like the one on the
      GNOME Clock, is added to this interface. When the pane is
      visible it shows the map and the options that the user can
      enter.
      - Users can add the location on the map, by pin-pointing
        the location. Users can add locations by coordinates or
        street address.
      - The map should show by default some user defined
        location when no localization method is available or
        automatically detect the users location.
- A localization preference option added to the main GTG! Interface.
  My suggestion is a menu for the plug-in options (Plug-in options,
  Localization preferences for example).
  - Here a user selects his default location for a starting point on
    the map.
  - Users also select the preferred location determination methods
    (GPS, Hostip, cell phone, etc).
- The plugin extends the workview concept and filters the tasks by
  location. A task that can be completed "right now" is a task that
  also matches the users current location.
  - A user should also be able to enable/disable this feature on the
    plug-in options.
- A new "map view" that will enable a pane with a map showing the
  users tasks.
  - This pane could have two columns. On one side there will be kind
    of a workview list of tasks and on the other a map with the
    tasks. (?)

## Geoclue python support

I prupose to create a python-geoclue lib/module that facilitates the
geoclue implemantation on any python project.

- Python-geoclue (pygeoclue) is under development. It's available at
  my launchpad branch
  [lp:~pcabido/+junk/pygeoclue](https://code.launchpad.net/~pcabido/+junk/pygeoclue).
- It currently supports:
  - Discovery of the current location
  - Get the available providers
  - Change the default position provider
  - Change the default address provider
  - Change the Client Requirements
  - Signal support to detect changes on the address or position
