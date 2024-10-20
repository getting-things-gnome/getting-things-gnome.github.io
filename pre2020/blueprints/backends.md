# Polish back-ends experience

Back-ends are already coded. Actually, there was much time invested in
this feature: [Luca's GSoC](../../gsoc/2010_invernizzi_portfolio),
[Madhu's GSoC](../../gsoc/2011_Madhu) and so on. The
purpose of this blueprint is to remove last few rough edges, make
programmers and users feel good about using back-end feature - give them
positive experience.

There are two levels we need to work on:

- *programmers* -- allow them to write full standalone back-end as
  fast as possible and as less pain as possible
- *users* -- synchronizing their tasks with their favorite on-line
  service without any hassle

## Programmers

List of problems (need to elaborate and propose solution):

Hello World back-end -- should be under 100 lines of code

We need to make it as simple as possible to get as many backends as
possible => another feature for GTG users.

United handling of errors, united behavior across backends

Special configuration parameters =>\> use fallback entry widget.

Specifying only important things:

- how to authenticate -- most of the services use similar 2-step
  system: 1, open the webpage 2, enter the code
- how to fetch list of current tasks, or the whole set of current
  tasks
- how to transform an online task into GTG task - sync online => GTG
- how to transform a GTG task into an online task - sync GTG => online

### Use cases

Irvine is a very talented high school student and he has created his own
online todo list. He heard about GTG which is used among Ubuntu users.
Irvine finds an tutorial "How to make GTG backend in 5 minutes" on GTG
blog and using method copy'n'paste he is able to make hack back-end for
his method in 30 minutes.

Mike is a big fan of GitHub. He decides to build a back-end
for GitHub. In the configuration dialog he can allow user to
specify the name of GitHub project to follow what other
backends usually don't use. Mike doesn't even notice there could be
problem with requesting parameter like this. In the parallel universe,
Mike is really angry, because he has to spend extra hour to find a way
around to specify GitHub project name parameter.

## Users

Handling features that are not available to online service: start date,
due date, subtasks; also additional parameters of online service like:
estimated time to finish, progress and so on.

Using GNOME's online config tool.

### Use cases

Peter gets a new smartphone and wants to synchronize his tasks with the
phone and the computer. He chooses one of the most famous services like
Remember the Milk, Google Tasks. He adds a new backend and his tasks are
magically synchronized everywhere.

