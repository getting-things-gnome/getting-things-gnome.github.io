# Quick Add Syntax Proposal

This proposal outlines a simple, unified syntax for adding tasks in GTG
via the Quick Add box. This simple syntax would allow power users to add
multiple tasks more quickly and efficiently - but doesn't require any
extra UI, so won't clutter the interface, confuse new users or be
onerous to implement.

The proposed syntax has only three elements: | for multiple tasks, \>\>
for subtasks and @ for tags.

## Multiple Tasks Syntax

Entering the following text into the Add box:

    Task One|Task Two|task3|Task Last

and pressing Enter or clicking 'Add' should create 4 new tasks, called:

     Task One
     Task Two
     task3
     Task Last

## Subtasks Syntax

Typing this into the Add box:

    Task1>>subtask1>>Subtask Two>>Sub-task 3

would create the following task:

    Task1

with the following subtasks created and assigned:

       - subtask1
       - Subtask Two
       - Sub-task 3

## Tags Syntax

Typing this into the Add box:

    Task One@pr@follow-up

would create this task:

    Task One

with the following tags attached:

    @pr, @follow-up

## Putting it all together

Ideally these features would all be implemented, so that entering this
into the Add bar:

    Task One@follow-up>>Sub Task One@pr>>Sub Task Two|Task 2|Task Three>>Subtask One|Task-the-last@personal

creates these tasks, with the indicated tags attached:

    Task One @follow-up
        - Sub Task One @follow-up, @pr
        - Sub Task Two @follow-up
    Task 2
    Task Three
        - Subtask One
    Task-the-last @personal

Note the tag inheritance to subtasks, with additional tags also applied.

### Character choices & possible clashes

If you're using characters from the standard International 101 keyboard
set (i.e. general ascii type stuff) and you're intending to mix this
with general text (i.e. more general ascii stuff) then you need to
acknowledge that this can't be done without an occasional clash, where
someone wants to use one of your special characters in their text. There
are several ways round this, none of them ideal: escaping, quoting, or
syntax rules. Of these, Syntax Rules - i.e. special characters are
always special, you just have to learn not to use them, seems to be the
best choice for this application. It's a very simple syntax and I'm only
proposing to use two extra special characters: '|' and '>\>', as '@' is
already special in GTG. These characters are very rarely used in normal
human language but have long precedent as special characters in command
line interfaces - where they've been used successfully for many years.

I've tried to stick with established command line norms for the syntax,
with one eye on using chars that probably won't occur in task titles
very often. This is why I suggested '>\>' for subtasks rather than '>'
or '-'. Both of those would probably occur in task titles at least
occasionally, and '>\>' is unix for append to file. It seems unlikely to
me that lots of people are using either '>\>' or '|' in task titles very
often (if ever) and even if they are, would probably be willing to
change in exchange for this functionality - I know I would, if I was
using them (which I'm not).

