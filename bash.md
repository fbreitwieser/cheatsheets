
## History expansion

```
## Print out command on command line on enter - don't execute immediately
shopt -s histverify # or M-^ for history-expand current line
```

```shell
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

## Parameter expansion

```
       The  `$'  character introduces parameter expansion, command substitution, or arithmetic expansion.  The parameter name or symbol to be expanded may be
       enclosed in braces, which are optional but serve to protect the variable to be expanded from characters immediately following it which could be inter-
       preted as part of the name.

       When  braces  are  used,  the  matching ending brace is the first `}' not escaped by a backslash or within a quoted string, and not within an embedded
       arithmetic expansion, command substitution, or parameter expansion.

       ${parameter}
              The value of parameter is substituted.  The braces are required when parameter is a positional parameter with more  than  one  digit,  or  when
              parameter is followed by a character which is not to be interpreted as part of its name.  The parameter is a shell parameter as described above
              PARAMETERS) or an array reference (Arrays).

       If the first character of parameter is an exclamation point (!), and parameter is not a nameref, it introduces a level of variable indirection.   Bash
       uses the value of the variable formed from the rest of parameter as the name of the variable; this variable is then expanded and that value is used in
       the rest of the substitution, rather than the value of parameter itself.  This is known as indirect  expansion.   If  parameter  is  a  nameref,  this
       expands  to  the  name  of the variable referenced by parameter instead of performing the complete indirect expansion.  The exceptions to this are the
       expansions of ${!prefix*} and ${!name[@]} described below.  The exclamation point must immediately follow the left brace in order to  introduce  indi-
       rection.

       In each of the cases below, word is subject to tilde expansion, parameter expansion, command substitution, and arithmetic expansion.

       When  not performing substring expansion, using the forms documented below (e.g., :-), bash tests for a parameter that is unset or null.  Omitting the
       colon results in a test only for a parameter that is unset.

       ${parameter:-word}
              Use Default Values.  If parameter is unset or null, the expansion of word is substituted.  Otherwise, the value of parameter is substituted.
       ${parameter:=word}
              Assign Default Values.  If parameter is unset or null, the expansion of word is assigned to parameter.  The value of parameter is then  substi-
              tuted.  Positional parameters and special parameters may not be assigned to in this way.
       ${parameter:?word}
              Display  Error  if Null or Unset.  If parameter is null or unset, the expansion of word (or a message to that effect if word is not present) is
              written to the standard error and the shell, if it is not interactive, exits.  Otherwise, the value of parameter is substituted.
       ${parameter:+word}
              Use Alternate Value.  If parameter is null or unset, nothing is substituted, otherwise the expansion of word is substituted.
       ${parameter:offset}
       ${parameter:offset:length}
              Substring Expansion.  Expands to up to length characters of the value of parameter starting at the character specified by offset.  If parameter
              is  @,  an  indexed  array  subscripted  by @ or *, or an associative array name, the results differ as described below.  If length is omitted,
              expands to the substring of the value of parameter starting at the character specified by offset and extending to the end of the value.  length
              and offset are arithmetic expressions (see ARITHMETIC EVALUATION below).

              If offset evaluates to a number less than zero, the value is used as an offset in characters from the end of the value of parameter.  If length
              evaluates to a number less than zero, it is interpreted as an offset in characters from the end of the value of parameter rather than a  number
              of  characters,  and  the  expansion  is the characters between offset and that result.  Note that a negative offset must be separated from the
              colon by at least one space to avoid being confused with the :- expansion.

              If parameter is @, the result is length positional parameters beginning at offset.  A negative offset is taken relative to one greater than the
              greatest  positional parameter, so an offset of -1 evaluates to the last positional parameter.  It is an expansion error if length evaluates to
              a number less than zero.

              If parameter is an indexed array name subscripted by @ or *, the result is the length members of the array beginning with ${parameter[offset]}.
              A negative offset is taken relative to one greater than the maximum index of the specified array.  It is an expansion error if length evaluates
              to a number less than zero.

              Substring expansion applied to an associative array produces undefined results.

              Substring indexing is zero-based unless the positional parameters are used, in which case the indexing starts at 1 by default.  If offset is 0,
              and the positional parameters are used, $0 is prefixed to the list.

       ${!prefix*}
       ${!prefix@}
              Names  matching  prefix.   Expands to the names of variables whose names begin with prefix, separated by the first character of the IFS special
              variable.  When @ is used and the expansion appears within double quotes, each variable name expands to a separate word.

       ${!name[@]}
       ${!name[*]}
              List of array keys.  If name is an array variable, expands to the list of array indices (keys) assigned in name.  If  name  is  not  an  array,
              expands  to 0 if name is set and null otherwise.  When @ is used and the expansion appears within double quotes, each key expands to a separate
              word.

       ${#parameter}
              Parameter length.  The length in characters of the value of parameter is substituted.  If parameter is * or @, the  value  substituted  is  the
              number  of  positional parameters.  If parameter is an array name subscripted by * or @, the value substituted is the number of elements in the
              array.  If parameter is an indexed array name subscripted by a negative number, that number is interpreted as relative to one greater than  the
              maximum index of parameter, so negative indices count back from the end of the array, and an index of -1 references the last element.

       ${parameter#word}
       ${parameter##word}
              Remove matching prefix pattern.  The word is expanded to produce a pattern just as in pathname expansion.  If the pattern matches the beginning
              of the value of parameter, then the result of the expansion is the expanded value of parameter with the shortest matching  pattern  (the  ``#''
              case)  or  the  longest  matching  pattern (the ``##'' case) deleted.  If parameter is @ or *, the pattern removal operation is applied to each
              positional parameter in turn, and the expansion is the resultant list.  If parameter is an array variable subscripted with @ or *, the  pattern
              removal operation is applied to each member of the array in turn, and the expansion is the resultant list.

       ${parameter%word}
       ${parameter%%word}
              Remove  matching  suffix  pattern.  The word is expanded to produce a pattern just as in pathname expansion.  If the pattern matches a trailing
              portion of the expanded value of parameter, then the result of the expansion is the expanded value of parameter with the shortest matching pat-
              tern  (the  ``%''  case)  or  the longest matching pattern (the ``%%'' case) deleted.  If parameter is @ or *, the pattern removal operation is
              applied to each positional parameter in turn, and the expansion is the resultant list.  If parameter is an array variable subscripted with @ or
              *, the pattern removal operation is applied to each member of the array in turn, and the expansion is the resultant list.

       ${parameter/pattern/string}
              Pattern substitution.  The pattern is expanded to produce a pattern just as in pathname expansion.  Parameter is expanded and the longest match
              of pattern against its value is replaced with string.  If pattern begins with /, all matches of pattern are  replaced  with  string.   Normally
              only  the  first  match  is replaced.  If pattern begins with #, it must match at the beginning of the expanded value of parameter.  If pattern
              begins with %, it must match at the end of the expanded value of parameter.  If string is null, matches of pattern are deleted and the  /  fol-
              lowing  pattern  may  be  omitted.  If the nocasematch shell option is enabled, the match is performed without regard to the case of alphabetic
              characters.  If parameter is @ or *, the substitution operation is applied to each positional parameter in  turn,  and  the  expansion  is  the
              resultant  list.   If parameter is an array variable subscripted with @ or *, the substitution operation is applied to each member of the array
              in turn, and the expansion is the resultant list.

       ${parameter^pattern}
       ${parameter^^pattern}
       ${parameter,pattern}
       ${parameter,,pattern}
              Case modification.  This expansion modifies the case of alphabetic characters in parameter.  The pattern is expanded to produce a pattern  just
              as  in  pathname  expansion.   Each character in the expanded value of parameter is tested against pattern, and, if it matches the pattern, its
              case is converted.  The pattern should not attempt to match more than one character.  The ^ operator converts lowercase letters  matching  pat-
              tern to uppercase; the , operator converts matching uppercase letters to lowercase.  The ^^ and ,, expansions convert each matched character in
              the expanded value; the ^ and , expansions match and convert only the first character in the expanded value.  If  pattern  is  omitted,  it  is
              treated like a ?, which matches every character.  If parameter is @ or *, the case modification operation is applied to each positional parame-
              ter in turn, and the expansion is the resultant list.  If parameter is an array variable subscripted with @ or *, the case modification  opera-
              tion is applied to each member of the array in turn, and the expansion is the resultant list.

       ${parameter@operator}
              Parameter  transformation.  The expansion is either a transformation of the value of parameter or information about parameter itself, depending
              on the value of operator.  Each operator is a single letter:

              Q      The expansion is a string that is the value of parameter quoted in a format that can be reused as input.
              E      The expansion is a string that is the value of parameter with backslash escape sequences expanded as with the $'...' quoting  mechansim.
              P      The expansion is a string that is the result of expanding the value of parameter as if it were a prompt string (see PROMPTING below).
              A      The expansion is a string in the form of an assignment statement or declare command that, if evaluated, will recreate parameter with its
                     attributes and value.
              a      The expansion is a string consisting of flag values representing parameter's attributes.

              If parameter is @ or *, the operation is applied to each positional parameter in turn, and the expansion is the resultant list.   If  parameter
              is an array variable subscripted with @ or *, the case modification operation is applied to each member of the array in turn, and the expansion
              is the resultant list.

              The result of the expansion is subject to word splitting and pathname expansion as described below.
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
