# Week 5 Report

For this week, I finally had a major breakthrough and I have the task
editor loading tasks properly (apart from one small bug that I have to
figure out, where in a group of subtasks it misses converting a subtask
into the proper format. It properly loads tasks, detects urls for
websites and bugs. It uses proper title formatting, as well. If you want
to check it out, I just uploaded the latest code and what you need to do
is go into GTG/gtk/editor/taskcontroller.py and there is some debug
lines at the bottom. Add in a task id into the 'open_task' line and it
will open that task for you.

