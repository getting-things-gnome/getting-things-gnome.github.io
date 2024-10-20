# Making GTG more Backend Friendly

**Abstract:**

Getting things Gnome, at present, is a simple task manager, with added
multiple backend support for other online and offline apps such as
Twitter, RTM, GNote, etc. My project focuses on adding diverse web based
backends for different use cases to GTG. Specifically, I’ll be adding
support for Google Calender, Tracks (web based, self hosted GTD
application), Github Issues, Bitbucket Issues and Redmine.

**Deliverables:**

The deliverables at the end of the project are:

1. Backend for Google Calendar
2. Backend for Tracks
3. Backend for Basecamp
4. Backend for Github issues
5. Backend for Bit Bucket issues
6. Backend for Redmine.
7. Documentation on writing backends

**Backend for Google Calender**

Google Calender keeps track of events. Sync GTG with GCal, and all your
events with the tags you want, will appear in GTG. Say a dear one’s
birthday in the next week shows up in GTG priorly. Ample time to get her
a gift isn’t it? The Google Calender API enables this GTG \<-> GCal
sync.

**Backend for Tracks**

Tracks is a web based application implementing the Getting Things Done
methodology, and is built on Ruby on Rails. Tasks are mapped as to dos
in tracks. The mapping is done using Rest API, that uses simple HTTP
requests. When the GTG user enables Tracks sync, your todos will surface
in GTG.

**Backend for Basecamp**

Basecamp is an extensively used online project collaboration tool.
Support for Basecamp to-do-lists in GTG will be added, using the REST
API.

**Backend for Redmine & Github/BitBucket issues**

Issue tracking is a necessary part of most people’s lives (most
developers atleast). While GTG has a backend for Launchpad already,
adding support for other popular issue tracking systems would increase
usage of GTG.

**Documentation for Writing Backends**

Documentation and samples to make it easier for other people to write
backends.

***Links:***

1.My Proposal: <http://goo.gl/ahcsF>

------------------------------------------------------------------------

2.Task Semantics: <http://goo.gl/IglAh>

------------------------------------------------------------------------

***Code***

Source Control Used: Bazaar <https://code.launchpad.net/~madhuvishy>

# Weekly Reports

***Week 1***

*This week:*

My target for the first two weeks is to complete the backend for Google
Calendar. I am using the GData Python Client Library that provides the
Google Calendar API, for this. As the generic backend framework is
already available, I only have to implement the backend specific
methods. At the lowest level is an GcalEvent, an object
that is an abstraction of the Calender Event. Then the
GcalProxy class that contains the methods that relate with
the backend to fetch or submit events. ClientLogin is
used to authenticate users.

*Next Week:*

Right now, I have only completed the framework for the Google Calender
backend. In the next week, I will complete the code, and establish two
way sync between GTG and GCal.

------------------------------------------------------------------------

***Week 2***

I have set up the UI for the Google Calender backend, which is now added
to the list of Backends in GTG \[1\]. I have also set up the GData
client library. I could not get any more code written as I was
travelling.

This week, I will invest time in further understanding GTG code, and
sharpening my basics, to enable me to write better code. I will also
complete the calendar backend, and get started on Google Tasks
integration.

Screenshot: \[1\] <http://min.us/mbpVCsqWXvSBnU> Code: \[2\]
<https://code.launchpad.net/~madhuvishy/gtg/added-google-calendar>

------------------------------------------------------------------------

***Week 3***

*This Week:*

I started with gaining a stronger foot on pygtk and python first. Then
with the help of my mentor, Luca Invernizzi, I understood how the
backends are structured, and started out to write code for the Google
Calendar backend for 2 specific use cases Adding tasks in GTG reflecting
in GCal and vice-versa Deleting tasks in GTG reflecting in GCal and
vice-versa And I've been successful in implementing both, excepting some
minor issues. I have updated the code on launchpad \[1\].

*Next Week:*

I will fix the issues with GCal, and also add Updating of tasks
functionality. Currently I have statically authenticated to a test
account, and will upgrade that to user authentication via OAuth or
ClientLogin. I hope to complete these early in the week
and get started with Google Tasks integration.

*Links:*

Code: <https://code.launchpad.net/~madhuvishy/gtg/added-google-calendar>

------------------------------------------------------------------------

***Week 4***

Last week, I continued the work on the Google Calendar sync. I have
added authentication feature using ClientLogin, by
modifying the UI suitably. I have added the update function, but having
trouble because the set_text method of GTG throws an error. Excepting
that, the GCal Backend is almost done!!

I invested time reading the basics of REST API, as most of the upcoming
backends use this API. I have also been reading up on Google Tasks API.

This week, I need to finally fix up GCal and move on quick. Will spend
sometime documentation on writing Backends. Then Google tasks and Tracks
integration should follow soon.

------------------------------------------------------------------------

***Week 5***

*This Week:*

Yeah! The Google Calendar Backend is close to complete
:) Now it is synced from
GTG to GCal and vice versa. There are some functionality I would like to
add though - such as tag specific import a nd export, find a way to add
Where and Guests values to the GTG task ( may be add them as subtasks),
allow users to switch between default calendar and other calendars.
These are on my wishlist, and will probably add them later! I have
linked the updated revision \[1\].

Also I started on Google Tasks - This use the REST API and serves as a
predecessor for the other backends - as all the others that ensue use
REST too :) So I set up
the UI, and the functionality will follow suit. Find link to the code
below \[2\].

*Issues:*

I had a few minor glitches such as, the events getting added into GCal
and returning the unique link, and the xml content perfectly, but the
event not showing up in the GCal UI. Also a date parsing issue while
importing into GTG. Will fix these after guidance from my mentor :)

*Next Week:*

The tasks backend should be up and about next week. The client libraries
are set up, the UI ready...

See you again next week, with the Google Tasks backend ready to go!

*Links*

\[1\] Updated Google Calendar: <http://bit.ly/kWaKjg> \[2\] Added Google
Tasks : <http://bit.ly/m6DIkn>

------------------------------------------------------------------------

***Week 6/7***

*Progress this week:*

I continued on the Google Tasks backend. I started out with registering
my application on the Google API console, which generated consumer and
developer keys for OAuth authentication. The Tasks API functions at 2
levels - Tasklists and Tasks. Each Tasklist is a group of tasks, and in
GTG, I had to only work at the Task level. Adding, Deleting and Updating
tasks, were pretty much the same as Calendar, with just different API
calls. So now the backend is up and working, and some fine tuning in
authentication, and choosing which task lists to import, should finish
it. The link to my code repo can be found below\[1\].

*Next Week:*

The next backend on my list is Tracks. However, I would first take a few
days to clean up code, write documentation and reports for the mid term,
before starting with Tracks.

\[1\] Code -
<https://code.launchpad.net/~madhuvishy/gtg/google-tasks-updated>

