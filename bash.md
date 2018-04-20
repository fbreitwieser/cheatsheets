
## History expansion

```
## Print out command on command line on enter - don't execute immediately
shopt -s histverify # or M-^ for history-expand current line
```

```shell
$ man  -P 'less -p ^HISTORY\ EXPANSION' bash
<...>
   Event Designators
       An  event designator is a reference to a command line entry in the history list.  Unless the reference is abso‐
       lute, events are relative to the current position in the history list.

       !      Start a history substitution, except when followed by a blank, newline, carriage return, =  or  (  (when
              the extglob shell option is enabled using the shopt builtin).
       !n     Refer to command line n.
       !-n    Refer to the current command minus n.
       !!     Refer to the previous command.  This is a synonym for `!-1'.
       !string
              Refer  to  the  most  recent  command  preceding  the current position in the history list starting with
              string.
       !?string[?]
              Refer to the most recent command preceding the current postition in the history list containing  string.
              The trailing ? may be omitted if string is followed immediately by a newline.
       ^string1^string2^
              Quick  substitution.   Repeat  the  previous  command,  replacing  string1  with string2.  Equivalent to
              ``!!:s/string1/string2/'' (see Modifiers below).
       !#     The entire command line typed so far.

   Word Designators
       Word designators are used to select desired words from the event.  A : separates the event  specification  from
       the  word designator.  It may be omitted if the word designator begins with a ^, $, *, -, or %.  Words are num‐
       bered from the beginning of the line, with the first word being denoted by 0 (zero).  Words are  inserted  into
       the current line separated by single spaces.

       0 (zero)
              The zeroth word.  For the shell, this is the command word.
       n      The nth word.
       ^      The first argument.  That is, word 1.
       $      The last argument.
       %      The word matched by the most recent `?string?' search.
       x-y    A range of words; `-y' abbreviates `0-y'.
       *      All  of the words but the zeroth.  This is a synonym for `1-$'.  It is not an error to use * if there is
              just one word in the event; the empty string is returned in that case.
       x*     Abbreviates x-$.
       x-     Abbreviates x-$ like x*, but omits the last word.

       If a word designator is supplied without an event specification, the previous command is used as the event.

   Modifiers
       After the optional word designator, there may appear a sequence of one or more of the following modifiers, each
       preceded by a `:'.

       h      Remove a trailing file name component, leaving only the head.
       t      Remove all leading file name components, leaving the tail.
       r      Remove a trailing suffix of the form .xxx, leaving the basename.
       e      Remove all but the trailing suffix.
       p      Print the new command but do not execute it.
       q      Quote the substituted words, escaping further substitutions.
       x      Quote the substituted words as with q, but break into words at blanks and newlines.
       s/old/new/
              Substitute new for the first occurrence of old in the event line.  Any delimiter can be used in place of
              /.  The final delimiter is optional if it is the last character of the event line.  The delimiter may be
              quoted  in  old  and new with a single backslash.  If & appears in new, it is replaced by old.  A single
              backslash will quote the &.  If old is null, it is set to the last old substituted, or, if  no  previous
              history substitutions took place, the last string in a !?string[?]  search.
       &      Repeat the previous substitution.
       g      Cause  changes  to  be applied over the entire event line.  This is used in conjunction with `:s' (e.g.,
              `:gs/old/new/') or `:&'.  If used with `:s', any delimiter can be used in place  of  /,  and  the  final
              delimiter  is optional if it is the last character of the event line.  An a may be used as a synonym for
              g.
       G      Apply the following `s' modifier once to each word in the event line.
```

## Keybindings
```
## Check keybindings
bind -lp

# In Emacs mode:
M-N M-. # Nth part of last command
M-0 M-. # last command name without arguments. Press repeatadly for history
    M-. # yank last argument of last command 

M-b   # word back
M-f   # word forward
M-d   # kill word

Cx -C-v  #display bash version
```
