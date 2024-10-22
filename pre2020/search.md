# Searching in gtg

## Abstract

Searching is, in a rough way, filtering the task tree to accommodate
what the user what he desires to see

## Implementation

Searches are implemented using the existing filter functionality of
[libarch](../libarch). A View Tree of the main task tree usually has one
or more filters applied. The main difference with the search filter is
that is by far the one that requires more user interaction.

A different view is used for searches so that we can always alternate
between both.

### Interface

searching, after many attempts and scrapped ideas, was defined as
instant filter applied as users are typing on the quickadd entry. when
there is no text in the entry, the main task pane shows the 'active'
view tree. typing text creates a new search object, filters the 'search'
view tree based on the input and switches the main pane to that view
tree.

as an added functionality, a valid search can be saved as a
[view](views), for quick custom filtering

### notation used

- @\[text\] - tags
- #\[text\]# - task titles (although if the plaint ext inputted on the
  entry matches a task title, its treated as such, even without the #)
- !\[text\] - commands
- "\[text\]" - literal searches (cans search for #, !, @, etc)
- \[text\] - free text ant title search
- dates - search for designated date, although the format of the dates
  is still not defined

### functionality

search for:

- specific tags
- specific tasks
- specific sequences of characters (through literals)
- specific due dates
  - now
  - soon
  - later
- interval of due dates
- states (active, done and dismissed)
- 

## Extending

### translations

Each of the commands used for filtering can be translated. On search.py
there is a set number of strings, two for each command. The first string
is for the base English keyword, and the second one is for added
translations. Overwriting the first would mean abandoning the original
base English keywords and only use localized ones. Overwriting the
translated keywords, would mean adding more keywords to the same kind of
filter. In the end, it's a mater of preference.

### Adding new Commands

it's highly recommended to use the command syntax (!\[keyword\]) when
extending, as using other notation would mean changing the regular
expression that handles the input from the quickadd Entry

new commands can be added by following this steps:

- adding the strings that represents the filter on search.py
- passing that string to the keyword dictionary on \_init_keywords
- creating the condition on build_search_tokens that accepts that word
  as a valid command and inserts the data used for filtering on the
  paramsToFilter variable
- creating the condition on the search filter that filters, search
  function on filteredtree.py

