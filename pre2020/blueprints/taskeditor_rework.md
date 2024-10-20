# Task Editor Rework

There are many bugs to solve about a task editor. Some of them requires
huge changes in code and therefore we want to create a new version of
task editor

## Related bugs

- [Have a link to the parent(s) in the task editor](https://bugs.launchpad.net/gtg/+bug/316922) (there is already some code)
- [Add tag, due and others via keyboard](https://bugs.launchpad.net/gtg/+bug/336603) (like RTM)
- [Create subtask with Keyboard](https://bugs.launchpad.net/gtg/+bug/339535) (\<Tab> may not recommended)
- [Tags' background color should be the tag's color](https://bugs.launchpad.net/gtg/+bug/339855)
- [Spell checking in the edit view](https://bugs.launchpad.net/gtg/+bug/341655)
- [Undo support in the task editor](https://bugs.launchpad.net/gtg/+bug/343328)
- [Autocomplete for tags](https://bugs.launchpad.net/gtg/+bug/343673) (With Tab or C-Enter better according to ploum)
- [Delete subtask but arrow left](https://bugs.launchpad.net/gtg/+bug/493335)
- [Creating a task in the task editor should support the quickadd syntax](https://bugs.launchpad.net/gtg/+bug/494389)
- [Drag and dropping tasks open in the taskeditor on to tags should refresh the content of the editor](https://bugs.launchpad.net/gtg/+bug/504874)
- [First line tags mess up the description](https://bugs.launchpad.net/gtg/+bug/504899)
- [Basic text formatting such as Bold, Italic, Underlined](https://bugs.launchpad.net/gtg/+bug/511938)
- [In task editor, there are accessibility problems like labels not associated with text edit controls for dates](https://bugs.launchpad.net/gtg/+bug/515355)
- [gtg_new_task does not support subtasks](https://bugs.launchpad.net/gtg/+bug/591130) (needs a split of GTK and parsing part)
- [Task with big attribute content causes huge memory uses](https://bugs.launchpad.net/gtg/+bug/618146)
- [Highlighting tags does not work properly](https://bugs.launchpad.net/gtg/+bug/754572) (Tag mis-recognition with ')', ',' or other notation behind)
- [Selecting a link opens the link in the browser](https://bugs.launchpad.net/gtg/+bug/823339)
- [convert selected lines to subtask by clicking the subtask button](https://bugs.launchpad.net/gtg/+bug/823879)
- [Workflowy mode for task editor](https://bugs.launchpad.net/gtg/+bug/826960) (Need more discussion, pure imitation is not elegant.)
- [Put into a clipboard also rich text version of copied task description](https://bugs.launchpad.net/gtg/+bug/830968)
- [Importing dashed lines should create subtasks immediately](https://bugs.launchpad.net/gtg/+bug/830971)
- [Simpleway how to input a lot of new tasks withing a certain structure](https://bugs.launchpad.net/gtg/+bug/887089)
- [removing non-existing subtask](https://bugs.launchpad.net/gtg/+bug/906374)
- [Minimal neweditor size for big toolbars](https://bugs.launchpad.net/gtg/+bug/936214)
- [Hiding a task editor after canceling delete](https://bugs.launchpad.net/gtg/+bug/959016)
- [Having a tag in subtask title the task "inherits" tags](https://bugs.launchpad.net/gtg/+bug/961331)
- [Context menu on an URL should have a "Copy Link Location" command](https://bugs.launchpad.net/gtg/+bug/961393)
- [tags in subtask subject lines seem to cause problems](https://bugs.launchpad.net/gtg/+bug/669479)
- ["-" + Enter would raise an error in Task Editor](https://bugs.launchpad.net/gtg/+bug/966614)
- [In-editor search](https://bugs.launchpad.net/gtg/+bug/966596)
- [User-definable Shortcut Key](https://bugs.launchpad.net/gtg/+bug/741454)
- [Hidden part of calendar](https://bugs.launchpad.net/gtg/+bug/1032745)

## Format of tag

Note:

-  There should be a list of allowned notations in tags which need more discussion.

Definition in Regular Expression (in Python):

- This is deprecated and will revised later.
- `re.complie('(?:^|\s)@([^!@\s]\S*)', re.MULTILINE)`

What should be a tag:

- @tag
- @google.com
- @M&M should be parsed as @M

What shouldn't be a tag:

- @@ -- it is a part of diff output
- <user@mail.com> -- not e-mail addresses
- @!tag -- '!' is reserved for negation of tags, it might interfere
  with tag completion
- @tag@ should not be a tag.

More specification:

- @should omit the notation at the end of sentence. e.g. "go @home."
  should be parsed as "@home" instead of "@home."

## Features summary

- Redesign task structure (This tends to solve a lot of strange bugs)
- Quick add syntax
- Tag auto-completion
- Undo
- Rich text format
- Spell check
- Faster way of adding subtask
- Search for text within a task-editor, and Search for Task using task
  browser
- User Definable Shortcut Key

## To Do List

- make a new structure of a task -> tags, subtasks, bold, italic
- split GTK and parser part (and write intensive tests for parser)
- implement undo & tag completition
- design when to autosave
- respond to modified() signal (auto refresh of a task)
- implement spell check
- design keyboard friendly way how to enter lot of subtasks (including
  nested subtasks) (something like workflowy mode)
- Disabled Mode (something like launchpad bugs list which is not
  allowed to edit title and content except for adding and deleting
  tags.)

### Tags removal

- remove tags only from tags line or when there is nothing more than a
  tag on on the single line
- other reocurrences replace by the name of tag

Example task:

    Call @boss @today
    @boss

    Discuss with my @boss my assignments.

After removing tag @boss

    Call boss @today

    Discuss with my boss my assignments.

## Some Opinions

- Refer to reStructuredText or some other markup language syntax
  - lists (subtask in GTG) start with dash and a space (nest also
    support)
  - rich text format // \\\*italic\\\*, \\\*\*blod\\\*\*, no
    underline syntax
- restrict some field value pattern to make it parsed by Regular
  Expression
  - Example: restrict tag start with @ and only contains letters,
    numbers or some limited symbol like '-'. // tag_pattern = re.compile('@\[\\w-\]+')
- Vim auto-completion
  - I am used to the raw auto-completion in vim and its display.
    More discussion needed.

## Conclusion

- Suggestions tend to realize features:
  - Redesign task structure
  - Quick add syntax
  - Rich text format
  - Tag auto-completion
- Features remained and some potential reference
  - Spell check
    - Pitijo's code
    - python-enchant
  - Undo
      - Luca's code

## Interested people

- huxuan
- [IzidorMatusov](https://wiki.gnome.org/IzidorMatusov)
- Song Yangyu

