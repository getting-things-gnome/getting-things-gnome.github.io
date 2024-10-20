# GTG's integration with GNOME Shell

by Baptiste Saleil

GTG is simply the better soft to manage personnal tasks with all
features a user needs. Also, I use the so friendly Gnome-Shell since the
begining of his young age. So, my idea is to work on GTG software, to
create the better link as possible between GTG in one side and
Gnome-Shell in the other one, to improve usage and rapidity. By this
way, the user could manage his tasks (Create, edit,...) directly from
the shell with a friendly and unified interface.

[Project page](http://google-melange.appspot.com/gsoc/project/google/gsoc2012/bsaleil/24002)
| [Full proposal](http://google-melange.appspot.com/gsoc/proposal/review/google/gsoc2012/bsaleil/9002)
- [pdf](http://baptiste.saleil.free.fr/gnome.pdf)
| [Extension repository](https://github.com/bsaleil/gtg-gnome-shell-extension)
| [Plugin repository](https://github.com/bsaleil/gtg-notification-plugin)
| [Blog](http://bsaleil.org/blog/?cat=6)

## Contact Information

Email: <baptiste.saleil@gmail.com>  
Website : <http://bsaleil.org/>  
Github profile : <https://github.com/bsaleil>  
Mentor : <http://www.lucainvernizzi.net/> (Luca Invernizzi)

# Extension for GNOME Shell

## Installation

This extension is available on GNOME Shell extensions website with the
name "GTG Integration". To install it, you can simply go to the website,
search for the extension, change the switch button to "ON", and accept
download. It is now installed. This extension bring many features
described in next section.

## Usage

### Search in overview

![search.png](http://bsaleil.org/blog/wp-content/uploads/2012/07/search.png)  
This feature is simple to use. Open the overview by pressing "super" key
or move your mouse on top left corner or click on "Activities" button,
type some letters to search in your tasks, and the extension will
displays results. The task editor will be open if you click on a task.

### Calendar menu

![calendar.png](http://bsaleil.org/blog/wp-content/uploads/2012/07/calendar.png)  
The second feature bring with the extension is the calendar menu which
can be open by clicking on the date in the topbar. For now, the GTG
calendar menu will replace the existing, synchornization of both is
planned for the future. This menu can be split in two others, tasks menu
and todo list.

#### Tasks menu

This menu shows GTG's tasks to do for selected day in calendar menu, on
the left. You can see two different colors for your tasks. The first one
(Grey) displays tasks which has start date identic to the day selected
and the second one (Dark grey) displays only tasks with a start date
before the day selected and/or a due date after the day selected.

#### Todo list

On the right side of the calendar menu is the todo list. This menu
displays only tasks without start date AND without due date. By this
way, every tasks are listed to user.

#### Preferences

![preferences.png](http://bsaleil.org/blog/wp-content/uploads/2012/07/preferences.png)  

# Plugin for GTG

## Installation

This plugin add possibility to be notified about your tasks on GTG.

\* Download archive, or clone repo  
\* Copy content on GTG plugins folder  
\* Active it on GTG  

## Usage

### Open time picker

![gtgtaskeditor.png](http://bsaleil.org/blog/wp-content/uploads/2012/08/gtgtaskeditor.png)  
If you open task editor for a task, you'll se a new button
("Notification") When you click it, the time picker is opened.

### Select time/date

![](http://bsaleil.org/blog/wp-content/uploads/2012/08/gtgtimepicker.png)  
Here you can chose a date/time to be notified for this task. Now you
just have to confirm and an job will be remotly created with at command.

### Notification

![gtg-notification.png](http://bsaleil.org/blog/wp-content/uploads/2012/08/gtg-notification.png)  
When job is executed, a python script (notifify.py) will be lauch and
notification will appear with "Edit" and "Done" button. For now, if GTG
is closed when you click on one of the two buttons, nothing will happen
so, GTG must stay open. If you click on "Edit" button, the task editor
will be open for this task. If you click on "Done" button, the task will
be mark as done on GTG.

# Reports

Reports are written directly by mail to my mentor every week. More
information about features on repos or blog.

<table>
    <thead>
        <th>Week</th>
        <th>Done</th>
    </thead>
    <tbody>
        <tr>
            <td>#1</td>
            <td>
- Set up new architecture (modules) for extension<br/>
- Search provider for the overview working
            </td>
        </tr>
        <tr>
            <td>#2</td>
            <td>
- Add new tasks list menu with basics features :<br/>
List tasks,<br/>
Open gtg button,<br/>
Today and tomorrow keywords,<br/>
Clickable tasks<br/>
- Css system theme<br/>
- Hide the old menu
            </td>
        </tr>
        <tr>
            <td>#3</td>
            <td>
- Add Todo list<br/>
- Fix CPU bug<br/>
- Fix disable bug<br/>
- List all of the tasks for day selected<br/>
- User experience stuffs<br/>
- Unit tests
            </td>
        </tr>
        <tr>
            <td>#4</td>
            <td>
- Set up translation system<br/>
- Import infos from Gnome-Shell ‘.po’ files.<br/>
- Split long name tasks<br/>
- Clean up
            </td>
        </tr>
        <tr>
            <td>#5</td>
            <td>
- Set up preferences system with ‘prefs.js’<br/>
- ‘Theme’ and ‘Hide menu’ preferences working<br/>
- Scrollbar on todo menu<br/>
- Tought about fuzzy keywords
            </td>
        </tr>
        <tr>
            <td>#6</td>
            <td>
- Scrollbar on tasks list menu<br/>
- ‘Long task’ and ‘number of days’ preferences working<br/>
- Align widgets and replace checkbox with switch button<br/>
- Some calendar menu UI improvement<br/>
- Cleanup
            </td>
        </tr>
        <tr>
            <td>#7</td>
            <td>
- Continue to work on calendar menu to fix known bugs, cleanup,...
            </td>
        </tr>
        <tr>
            <td>#8</td>
            <td>
- Prepare GUADEC<br/>
- Write documentation<br/>
- Try new algorithms to improve performance<br/>
- Thinking about the notification system
            </td>
        </tr>
        <tr>
            <td>#9</td>
            <td>
- GUADEC week<br/>
- Training with python, gtk, at command,...<br/>
- Implement basics of notification system.
            </td>
        </tr>
        <tr>
            <td>#10</td>
            <td>
- First prototype :<br/>
- Possibility to select time/date for a task and record it into the task<br/>
- New script to launch notification with given infos and two buttons
            </td>
        </tr>
        <tr>
            <td>#11</td>
            <td>
- Notification system is now working with :<br/>
- Possibility to chose a date/time for a task<br/>
- Notification infos are correctly recorded in the task<br/>
- A job is created with a script which launch at command<br/>
- This job launch notify script to display notification<br/>
- "Edit" and "Done" button are working
            </td>
        </tr>
        <tr>
            <td>#12</td>
            <td>
Last week!<br/>
- Fix known bugs<br/>
- Add features (remove notification, disable UI when notification displayed,...)<br/>
- Write documentation on repos and wiki page<br/>
- Crying because the GSoC is over
            </td>
        </tr>
    </tbody>
</table>


## Blogged reports

[Project category in blog](http://bsaleil.org/blog/?cat=6)

# And after GSoC ?

After this summer, I'll continue to work on the extension and the
plugin. There are known bugs, and requested features. So, this is only
the beginning of my work. Moreover, I have some ideas for GTG and I'll
continue to work on it in the future.

Thanks [Luca](http://www.lucainvernizzi.net/)  
Thanks [GNOME](http://www.gnome.org/)  
Thanks [GSoC](http://code.google.com/soc/)

