# views

## abstract

Views are searches, saved in a internal format for quick retrieval

## Implementation

Searches are search (from search.py) parameters that are saved between
instances of \[gtg\] and re-filter the search tree when the

At this point (version 2.9 of gtg), it's still not certain if
views are better implemented as different views of the task tree
(avoiding re-filtering of the search tree). As for now, search tree view
is always re-filtered when calling the view.

### how are views stored

only the name of the view and the parameters to give the search filter
are necessary. Even the name can change between instances of the
gtg, as long has it doesn't exist already.

views are stored in the config file of gtg. A better implementation
would be a XML file containing the necessary data

### between instances

when started, gtg checks the config file for saved views and
appends the necessary nodes to tag tree. This is all done on
treefactory.py

## Interface

After input on the quickadd Entry, if a search is valid (has no syntax
errors), a popup action appears that gives the user the option to save
that search as a view. That view

Views are then given a name by the user (each name has to be unique, gtg
ensures of this by numerating the name case it already exists) and added
as child nodes of the search node (named... search) on the tag tree.

