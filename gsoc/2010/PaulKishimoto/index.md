# Getting Things GNOME! Summer of Code 2010 — Paul Kishimoto

- (My [Portfolio](portfolio) has its own page)

## Revised Proposal

### Goal

- To improve integration with complementary applications and support a
  wider variety of user workflows, blueprint and begin a transition of
  GTG from a monolithic to a client/server model, with communication
  over DBus.

### Rationale

Transitioning GTG! from a monolithic to a client-server model offers
internal and external advantages.

The chief internal advantage is clarity in the explicit separation of
user interface from the underlying data model and storage logic. In
particular, a GTG! server would be a much smaller collection of code
with fewer dependencies, and thus easier to cover with a comprehensive
test suite.

Also, changes to the user interface (bugfixes or improvements) could be
distinguished by whether or not they demanded extension of the DBus
interface. If they *did* require such changes, it would prompt an
discussion of the question, "Should this user case be handled by the UI
in a different way, or does it identify a shortcoming of the data
model." Bugs *not* requiring DBus API changes, on the other hand, could
be fixed by developers especially familiar with the GTG client UI.

External advantages include the possibility of supporting multiple UIs,
in particular the web-based UI proposed by Karlo Jež for his GSoC 2010
project. Also, the potential for collaboration with other tools that
expose or consume DBus interfaces — for example, Hamster, Tomboy/Gnote
and GAJ/Zeitgeist — would be improved. The simplicity of a
well-documented DBus API will encourage developers of these others
application to, in turn, improve collaboration with GTG!. This process
can be kick-started as part of my work by contributing patches to those
applications.

Finally, GTG developer discussion around user cases and data model can
inform a wider conversation on how the overall GNOME desktop experience
can better suit itself to the way users *actually* want to work and
play.

### Schedule

- Week 1
  - Learn about DBus, including current GTG interface, interfaces of
    other applications.
  - Map the GTG data model, with notes on key discrepancies with
    other tools.
- Week 2
  - Enumerate user cases for task & work tracking.
  - Develop a proposed GTG data model, including any modifications.
- Weeks 3-4
  - Identify current code segments in GTG as "client", "server", or
    "mixed".
  - Spec a DBus API which supports all current calls between
    "client" and "server" segments.
  - Draft a proposal for shared, pan-GNOME (or f.d.o?) task/work
    tracking semantics.
- Weeks 5-6
  - Code a test suite against the proposed DBus API.
- Weeks 7-8
  - Code GTG server infrastructure implementing DBus API
  - Continuous testing of above; add some tests for multi-backend
    behaviour.
- Weeks 9-10
  - Refactor GTG UI piece-by-piece to use DBus instead of Python
    calls.
- Weeks 11-12
  - Prepare & submit final report.
  - Revise draft proposal on GNOME task semantics.

------------------------------------------------------------------------

## Initial Proposal

- *Copy-and-pasted from my GSoC application.*

For the Google Summer of Code 2010, I am proposing work on the Getting
Things GNOME! task management application ("GTG"), as suggested at
[http://live.gnome.org/SummerOfCode2010/gtg-backends](../backends). By continuing my
involvement as a contributor to GTG, I will design and implement
software integrating GTG with many web-based task tracking tools,
allowing GTG to become an easy-to-use and natural part of GNOME users'
workflow.

As an aerospace engineering student, both my undergraduate and graduate
coursework and thesis research have contributed to my skill as a
developer. In order to practice good engineering, especially in the
areas of computational fluid dynamics and unmanned vehicle control, one
must have an easy facility with programming so that one can concentrate
on the scientific theories without stumbling over the code one is using
to study them. I have worked to cultivate such an ability, including
familiarity with best-practices software design concepts, proper use of
version control, and fluency in C, C++, Fortran, PHP, Python and
bash/dash shell scripting.

Beyond my academic life, however, I am an active user of and contributor
to Ubuntu and many GTK+ and GNOME applications I have discovered through
it. In addition, I have served as Webmaster or Communications Director
for a number of organizations, including the University of Toronto
Engineering Society, an organization of 4500 members. In this role I
have developed web services based on Free software including Drupal and
Moin Moin, which has included familiarizing myself with the APIs and
codebase of each in order to develop custom extensions.

My involvement with GTG has stemmed from my enthusiasm for its potential
as a tool. I developed the implementation of its preferences dialog,
including a rewrite of its plugins management interface
(<https://code.launchpad.net/~khaeru/+branches?field.lifecycle=MERGED);>
one merge (<https://code.launchpad.net/~khaeru/gtg/prefs-dialog>) landed
1190 lines of code.

A common theme in the above work is my ability for collaboration with
other developers. In every instance I have found that a voracious
appetite for reading other people's code and API documentation has
supplied me with knowledge that has streamlined software development and
allowed me to creatively reuse of others' work.

### Proposed Work

The work of integrating GTG with existing applications and improving its
user experiences involves three distinct areas of work and attendant
planning, as detailed below.

**First**, a detailed survey of existing planning and Getting Things
Done (GTD) tools is required. The GTG data model recognizes certain
tasks concepts—start and due dates, fuzzy dates ("now", "soon",
"later"), single-parent hierarchy, multiple tagging, task completion,
and task note text.

When other services are GTD-focused, they recognize overlapping concept
sets that also include concepts not included in GTG—for example, partial
completion, estimated time-to-complete, and multiple-parent hierarchy.

There are also applications with similar aims to GTG that are not
GTD-focused. Examples include the GNOME Activity Journal (formerly GNOME
Zeitgeist, <http://live.gnome.org/action/show/GnomeActivityJournal>),
which provides an interface to Tracker metadata and a timeline of user
actions; and Project Hamster (<http://projecthamster.wordpress.com>), a
more work-focused application that automates fine-grained time-logging.

These are both journalling applications that track current & past
activity, whereas GTG is a planning tool. Nevertheless, to a user
engrossed in his or her work, future plans flow seamlessly into present
work and the recorded past. The user's software should mirror this
behaviour, so closer integration of GTG with these tools is required.

Similarly, Planner (<http://live.gnome.org/Planner>) is a Gantt-model
application for large-scale project planning. Many users consider them
parts of a whole; so their individual workload (GTG) should be easily &
closely linked to any projects (Planner) of which they are a part.

In partnership with the GTG developers, I will distinguish cases where
the current state-of-the-art tools motivates changes to the GTG data
model, from cases where GTG can simply access the APIs or provide easy
opportunities to conditionally invoke other applications.

An attendant benefit of this survey will be that the popularity, concept
map and API features of each application and service will provide
evidence on which to determine the relative priority of various plugins
in GTG, as well as the expected difficulty and time to implement them.
This information will be useful to contributors who may desire tool
integration which do not fit with the scope of my GSoC 2010 work; for
example, potential GSoC 2011 participants. By documenting my process as
I make these determinations, I will also provide assistance to future
contributors wishing to, for example, update GTG to match the progress
of integrating the Activity Journal into future versions of the GNOME
desktop.

**Secondly**, the user interface of GTG itself must be considered. As an
example, some thoughts I proposed on a user interface for selecting and
controlling backends (<https://bugs.launchpad.net/gtg/+bug/336623>)
involve creative use of custom GtkCellRenderers.
These enhancements follow the principle that wherever possible, the
features of GTG must be invisible to the user, quietly supporting
instead of forcing jarring changes in the way (s)he works.

To provide tangible help to the GTG developers, I will enumerate a list
of test cases, and endeavour to provide both automated testing (by
adopting one of the many available Python unit testing tools,
<http://pycheesecake.org/wiki/PythonTestingToolsTaxonomy>) and user
tests (using Mago and the Linux Desktop Testing Project) to verify GTG's
behaviour in the presence or absence of the complementary tools listed
above.

I will also enlist user input by soliciting testing feedback from a mix
of experienced and inexperienced users, in order to ensure that support
and cues in the GTG interface allow an easy recognition and use of its
many features.

**Thirdly**, the technical work of integration with existing tools will
involve using the information gleaned in the first work area to provide
plugins, backends and enhancements to GTG core.

While this work will occur before or in parallel with the prior two
areas, it is a collection of more straightforward programming tasks. By
exploiting the modularity, MVC-style separation and DBus interface
already present in GTG, I can work simultaneously on a number of
different lines of integration.

This work may also involve submitting patches to the other GNOME desktop
tools with which GTG is to be integrated, in order to enhance their
APIs.

To these tasks I will bring the careful consideration, thoroughness, and
reference to best practice that allowed me to introduce the GTG
preferences dialog with minimal revisions to my initial proposed merge.

### Timeline

A timeline follows. Semi-weekly (or more frequent) blog posts
documenting progress will continue throughout.

#### Weeks 1-2 (24 May) — start

- Begin GTD tool survey, involving gtg-users mailing list
- Activity Journal, Tracker, Hamster & Planner codebase & API familiarization.
- Python testing tool evaluation.
- Mago & LDTP learning & familiarization.
- Setup Personal Package Archive & test packages for user involvement.

#### Weeks 3-4 (7 June)

- Complete application/tool survey, discuss & report results with GTG
  contributors & developers.
- Prototype joint usage models & distinctions with a "GTG-only" use
  case.
- Initial user testing implementation (on unaltered GTG codebase) &
  call for participants.
- Enumerate automated test-cases.

#### Weeks 5-6 (21 June)

- Automated testing implementation.
- Begin patches to other task/planning applications necessary for GTG integration.
- GTG plugins for application integration, first cut.
- Continue soliciting user testing.
- User interface design & scaffolding within GTG.

#### Weeks 7-8 (5 July)

- Summarize first-phase user testing results.
- Implement UI changes.
- Update user & automated testing to include application integration use-cases.
- Prepare midterm evaluation: present usable test release of Week 5-7 results.
- Call for participants in second-phase testing.

#### Weeks 9-10 (19 July)

- Modify GTG enhancements to degrade gracefully (if necessary patches
  to other applications are still pending).
- Documentation!
  - End-user help content & UI-inline tweaks.
  - Report on user testing.
  - Bug triage & other response to user feedback.
- Prototype and/or code low-priority GTG plugins for application
  integration.

#### Weeks 11-12 (2 August)

- Prepare & submit final report.

### Conclusion

Throughout my education I have come in contact with fantastically
expensive engineering software—MATLAB, AutoCAD, Solidworks, Aspen,
Blackboard and others being among others costing thousands of dollars
per instance. My horror that important, basic research and the education
of future engineers should be hobbled by such prohibitive costs has
contributed strongly to my enthusiasm for Free software. I believe in
the potential of Free development to produce tools that conform to our
behaviour as human beings, instead of distorting it to produce profit
for a few.

As I continue my engineering career, I know that wherever possible I
will use Free tools for my work, and develop them where they do not yet
exist. Working on GTG as a GSoC 2010 participant would be an auspicious
first step on this path.

