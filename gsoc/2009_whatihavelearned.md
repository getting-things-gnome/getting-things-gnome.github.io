# What I have learned

This is a kind of general report of SoC. The idea is to share all the
things I have done until now, what I have learned.

## Pre-SoC

I had a pretty good idea of what I wanted to do, just didn't know how to
do it yet. My idea for what I was planning to do you can read
[here](2009_idea).  
At this point I thought if I was going to work with Geoclue I would get
my hands into it. I took some time to read about
[Geoclue](http://www.freedesktop.org/wiki/Software/GeoClue), see how it
works, its properties, learn about the providers, get up to date with
it.  
So my first step was compiling Geoclue. I dind't have any trouble
compiling Geoclue, I had to compile
[Gypsy](http://gypsy.freedesktop.org/wiki/) first to have that provider
and I also had to install some developer packages (I use Ubuntu and
except for Gypsy they were all in the repositories).  
I checked the examples that were provided with Geoclue but they were all
written in C. They where a good help to see how the different providers
worked.

I was also reading about SoC and looking into the community. IRC was a
starting point and it was easy to talk to other people there. At this
point I was receiving lots of e-mails on the SoC list, hundreds of
e-mails a day and of course I wanted to read all of them. I confess, it
wasn't possible. I started to filter the important ones and reading
those only. Only after a few weeks was I able to read all or most of all
the e-mail.

## SoC

By the end of the "bonding with the community" period I started to code.
Lionel (my mentor) was excited in seeing some code and I also wanted to
"get my hands dirty" so I started to code some examples in python to
show and learn how Geoclue could be used. This wasn't that easy at start
because I had never used D-Bus and there were no Geoclue + python
examples available.  
I went to google and quickly found this [python-dbus
tutorial](http://dbus.freedesktop.org/doc/dbus-python/doc/tutorial.html).
I also had to go thru the [Geoclue API
(D-BUS)](http://folks.o-hand.com/jku/geoclue-docs/). I then managed to
make some examples, four to be exact that are available
[here](http://paulocabido.com/soc/geoclue-examples/).  
I learned the importance of the Geoclue Master provider, internally the
Master provider uses the best Geoclue provider (based on client
requirements and provider availability, accuracy and resource
requirements). The provider that is actually used may change over time
as conditions change, but the client can just ignore this. This was
exactly what I wanted.

I was prepared to start changing GTG! and had a (more) serious meeting
with Lionel to discuss how this would be done. It was his idea and he
suggested a plugin. Of course to do the plugin the plugin support needed
to be done. This would be good for me as I had never done such a thing
and for GTG! that would be supporting plugins.

So I started to implement the plugin system/engine on GTG!. This was
hard at start because I didn't understand how a plugin system worked and
I didn't find nothing explaining, generically, how these systems worked.
I did in fact find some specific information that helped me:

- [The Gedit Plugin HowTo](http://live.gnome.org/Gedit/PythonPluginHowTo)
- [Tomboy - How to create addins](http://live.gnome.org/Tomboy/HowToCreateAddins)

These two pages helped allot, I had a better idea but I was still a
little confused on how the plugin would change the GTK+ interface. The
answer was easier than I imagined and I took more time searching and
looking into other applications code trying to understand this. I also
got a precious help from Jonathan Barnoud (aka Pititjo) who mailed me
some info and pointed me in the right direction for importing python
files as modules.

### The Plugin Engine

The general understanding of a plugin engine wasn't a problem, but the
specific understanding of how plugins would interact with GTK+ was hard
for me. At the end it was allot easier than I initially thought.  
A plugin engine has to load plugins, that's the idea right?! The first
thing is to decide how these plugins are going to be structured. GTG! is
written in python and the contributers are python developers so it only
made sense for the plugins to be python modules.  
So I decided that the plugins for GTG! would have the following
structure/properties:

- A plugin can have several classes, even several files but there is
  only one main class to the plugin and that is the class that handles
  the plugin. The difference between the main class and the others is
  that the main class has the following properties:
  - PLUGIN_NAME - Defines the plugin name.
  - PLUGIN_AUTHORS - Defines the plugin authors
  - PLUGIN_VERSION - Defines the plugin version
  - PLUGIN_DESCRIPTION - Defines the plugin description
  - PLUGIN_ENABLED - A boolean, that defines the default state of
    the plugin (enabled/disabled)
- A plugin has three mandatory methods, all plugins must have these
  methods, even if they aren't needed! All three methods receive a
  plugin api object as a parameter (I'll explain it down the way).
  - activate - This method will be executed when a plugin is
    activated. It will interact with the main GTG! window
    (TaskBrowser) and when the plugins are enabled
    they will be activated during the GTG! load
    (TaskBrowser load). It will also be executed
    when a plugin is activated during GTG! use.
  - deactivate - This method will be executed when a plugin is
    deactivated/disabled. It should reverse all changes that a
    plugin has done to GTG!.
  - onTaskOpened - GTG! has a additional "challange", the
    TaskEditor. When a task is opened GTG! opens a
    new window (TaskEditor) and this window is also a
    target for a plugin. So this method will be executed when a task
    is opened and the plugin api methods will reflect on this
    window.
  - A simple example:
    ```python
    class ExamplePlugin:
        PLUGIN_NAME = 'Example'
        PLUGIN_AUTHORS = 'Paulo Cabido <paulo.cabido@gmail.com>'
        PLUGIN_VERSION = '0.1'
        PLUGIN_DESCRIPTION = 'Plugin Description goes here.'
        PLUGIN_ENABLED = True

        def activate(self, plugin_api):
            pass
            
        def onTaskOpened(self, plugin_api):
            pass
                    
        def deactivate(self, plugin_api):
            pass
    ```

The plugin engine handles the loading of the modules and also the
unloading (when a plugin is deactivated) and when it should happen. The
LoadPlugins method does the tricky part. As I mentioned
before, Jonathan Barnoud pointed me in the right way. He mailed me the
code (those three lines of the first for) that would load python files
as modules. The modules pkgutil and imp are used to discover modules in
the plugins directory.

```python
def LoadPlugins(self):
       plugins = {}
       try:
           for loader, name, ispkg in pkgutil.iter_modules(self.plugin_path):
               file, pathname, desc = imp.find_module(name, self.plugin_path)
               plugins[name] = imp.load_module(name, file, pathname, desc)
       except Exception, e:
           print "Error: %s" % e
           
       for name, plugin in plugins.items():
           self.Plugins.append(self.loadPlugin(plugin))
                       
       return self.Plugins
```

I have talked about the plugins, how they are structured, how they are
loaded but another important part is how they interact with GTG!. This
is done thru the Plugin API. It would be easy to pass the GTK+ window to
the plugin and let the plugin developers do what they want, but that's
not a very good practice. So I created this API, that has the methods
that the plugins can use to interact with GTG!. The API supports the
following methods:

- AddMenuItem(item) - Adds a menu item to the main GTG! window's menu bar, under Plugins.
- RemoveMenuItem(item) - Removes a a menu item from the Plugin menu, at the menu bar.
- AddToolbarItem(item) - Adds a button to the main GTG! toolbar.
- RemoveToolbarItem(item) - Removes a button from the main GTG! toolbar.
- AddTaskToolbarItem(item) - Adds a button to the task editor's toolbar.
- getRequester() - Returns the requester object.
- changeTaskTreeStore(treestore) - Changes the tree store. This method
  was created to let plugin developers create new views for tasks.
- add_tag(tag) - Adds a tag to a task. This method is intended to be
  used within the task editor.
- add_tag_attribute(tag, attribute_name, attribute_value) - Adds a new
  attribute (and value) to a task. It appends the tag to the end of
  the task.
- get_tags() - Retrieves all tags of a task. This method is also
  intended to be used within the task editor.
- get_textview() - Passes the task editor's textview.

The API is a work in progress and things may change with time, some
methods can be altered and some new ones can be included. If you have
any suggestions, feel free to let me know.

The last part there is to talk about is the Plugin Manager. This is the
GUI to select witch plugins are enabled or disabled. The manager uses
the engine to activate/deactivate the plugins. It is accessible under
the Plugin menu (Preferences).

- [A image of the Plugin Manager in action](http://paulocabido.com/soc/mockups/plugin_manager_gui.png)

### python-geoclue

I have mentioned the examples I made to show how Geoclue can be used.
After writing those examples, I decided to write a module to help python
developers use Geoclue.  
The idea of the module is to facilitate as much as possible, for a
developer to use Geoclue without having to reinvent the wheel or help a
developer who lacks the time to learn about Geoclue from zero. This way
the only thing a developer needs is to import the module on their
project and with a minimum code effort they can get addresses and
positions.  
While coding this module (and the examples also) I learned about Geoclue
and D-Bus, witch I had never used. It's really easy to use.  
I also used signal/slots for the first time with the traditional
connect(function) method. This way it's possible to detect changes to
the address or position and automatically process those changes. I
thought about using D-Bus to make this but my idea was to have as less
dependencies as possible for the programmer.  
Currently this module is working with the following features:

- init() - I separated this from the init to be possible to use the
  Signals before any addresses or positions where detected.
- set_requirements(accuracy, time, require_updates,
  allowed_resources) - Changes the requirements for the provider.
- get_location_info() - Returns the variable (dictionary) with the
  location info (position and address). The values may vary with
  different providers.
- get_available_providers() - Returns a List of the available
  providers and witch services each provider supports.
- set_position_provider(provider) - Changes the position provider to a
  given provider.
- set_address_provider(provider) - Changes the address provider to a
  given provider.
- get_position_provider() - Returns the current position provider.
- get_address_provider() - Returns the current address provider.
- connect(function) and disconnect(function) - Connect or Disconnect
  (a already connect) function to handle changes on the location
  variable.
- compare_position(latitude, longitude, proximity_factor) – compares
  two positions, a given one and the actual position to see if they
  are the same or near by. The range is defined by the
  proximity_factor.
- reverse_position(latitude, longitude, accuracy) – Reverses a
  position to a address.

There is a test file in the test folder that I created to show how to
use each of these features. You can see for yourselves how easy it is to
use Geoclue now!  
Any suggestion or idea, as usual, is welcome.

## GTG

I have also learned allot about [Getting Things Gnome!](..). It is a well structured application
with a high potential!  
As you know, Getting Things Gnome! is an organizer for the GNOME desktop
environment. You create tasks to organize what you have to do and each
task can have subtasks and so on. For a task to be completed all the
subtasks (if they exist) also have to be completed. GTG! has a view
called "Work View" that lists the tasks that are possible to be
completed at that moment. So if a task with several subtasks exists, the
subtasks have to be completed before the main task will appear in the
"Work View". This is a great concept that lets one keep in mind the
priority of the tasks that are to be done.

So how does GTG! work?

- backend - The current implementation of the backend is the localfile
  (only existing backend for now). Tasks will be stored in a XML file.

- The core module, 'core' in GTG/ is the heart of the application and
  it contains:
  - the datastore synchronizes itself, on each start, with the
    backend. It contains a list of tasks (objects).
  - the requester. Because nothings interacts directly with the
    datastore, each interface uses the requester to
    translate/control the requests before sending them to the
    datastore. Only the requester can interact directly with the
    datastore.
  - task - It's a object with attributes (duedate, title, tags,
    parent, child, etc). The parent and child attributes define if a
    task is a subtask of another task. Each task has a tid (task id)
    and the tid is represented for example like 7@1. 7 is the task's
    number and 1 is number of the backend.
  - tags - Tags are also objects with attributes. The tags
    attributes are extensible. A tag is represented by "@tag" and an
    attribute example is color (witch has a value associated).
- TaskBrowser - It's the main GTG! window. When
  starting it asks the requester for a list of tasks, they are then
  displayed.
- TaskEditor - It's the particular view of a task.

