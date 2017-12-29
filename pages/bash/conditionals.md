---
title: Conditional Statements
tags: [tutorial]
keywords: bash, conditionals, if
last_updated: December 29, 2017
summary: Testing for specific conditions in your script
toc: true
sidebar: bash_sidebar
permalink: bash_conditionals.html
folder: bash
---

{% include note.html content="__[ ] vs. [[ ]]__<br />
Contrary to __[__, __[[__ prevents word splitting of variable values. So, if VAR='var with spaces', you do not need to double quote $VAR in a test - even though using quotes remains a good habit.
<br /><br />
Also, __[[__ prevents pathname expansion, so literal strings with wildcards do not try to expand to filenames. Using __[[__, the __==__ and __!=__ expressions will interpret strings to the right as shell glob patterns to be matched against the value to the left. For example, __[[__ 'value' == val* __]]__ would evaluate to true." %}

## if-then statement

### Description

The *if* statement allow you to test whether a condition is true or false in your
script.  *If* the test evaluates to true, *then* the script will execute any command
that is enclosed within the *if* statement block.  If it is false, the commands
inside that block will be ignored.

### Format

>if __TEST-COMMAND__; then<br />&nbsp;&nbsp;__CONSEQUENT-COMMANDS__;<br />fi

The __TEST-COMMAND__ list is executed, and if its return status is zero,
the __CONSEQUENT-COMMANDS__ list is executed.  The return status is the exit
status of the last command executed, or zero if no condition tested true.

The __TEST-COMMAND__ often involves numerical or string comparison tests, but it
can also be any command that returns a status of zero when it succeeds and some
other status when it fails. Unary expressions are often used to examine the
status of a file. If the FILE argument to one of the primaries is of the form
/dev/fd/N, then file descriptor "N" is checked. stdin, stdout and stderr and
their respective file descriptors may also be used for tests.

The __CONSEQUENT-COMMANDS__ list that follows the then statement can be any
valid UNIX command, any executable program, any executable shell script or any
shell statement, with the exception of the closing fi. It is important to
remember that the then and fi are considered to be separated statements in the
shell. Therefore, when issued on the command line, they are separated by a
semi-colon.

### Examples

```sh
#!/bin/bash
read value

# The use of double-brackets only works in BASH, KSH, and ZSH shells
if [[ $value < 5 ]]; then
    echo "Less than 5."
fi

# The use of single-brackets requires a system that is POSIX compliant
if [ "$value" -gt 5 ]; then
    echo "Greater than 5."
fi

# The test built-in accepts several switches which will be described later
if test "$value" -eq 5; then
    echo "Equal to 5."
fi
```

{% include tip.html content="If you enclose an expression in single-brackets as
shown in the second example above, always enclose a variable in
double-quotations.  This prevents wordsplitting and glob expansion. With
double-brackets as shown in the first example, this doesn't occur and thus
the double-quotations aren't necessary." %}

## if-then-else statement

### Description

This statement allows you to define an alternate action if the condition being
evaluated is false.

### Format

>if __TEST-COMMAND__; then<br />&nbsp;&nbsp;__CONSEQUENT-COMMANDS__;<br /> else
 <br />&nbsp;&nbsp;__ALTERNATE-CONSEQUENT-COMMANDS__;<br /> fi

Like the __CONSEQUENT-COMMANDS__ list following the then statement, the
__ALTERNATE-CONSEQUENT-COMMANDS__ list following the else statement can hold
any UNIX-style command that returns an exit status.

### Examples

```sh
#!/bin/bash
if [ $(whoami) ] != 'root' ] && [ -f "$1" ]; then
    echo "You entered $0 $1"
else
    echo "Root can'd do that!" # tongue in cheek
fi
```

## if-then-elif-else statement

### Description

This construct allows you to test for a secondary condition if the first
condition evaluated to false but before the catch-all else clause.

### Format

>if __PRIMARY-TEST-COMMAND__; then<br />&nbsp;&nbsp;__CONSEQUENT-COMMANDS__;<br />
elif __SECONDARY-TEST-COMMAND__; then<br />&nbsp;&nbsp;__MORE-CONSEQUENT-COMMANDS__;
<br />else<br />&nbsp;&nbsp;__ALTERNATE-CONSEQUENT-COMMANDS__;<br />fi

{% include note.html content="You can use as many *elif* clauses as you need, as
long as they are placed before your else clause. Generally though you want to ensure
that your *elif* clauses must be executed when the *if* clause fails (as opposed
to being a separate statement altogether)." %}

The __TEST-COMMANDS__ list is executed, and if its return status is zero, the
__CONSEQUENT-COMMANDS__ list is executed. If __TEST-COMMANDS__ returns a
non-zero status, each elif list is executed in turn, and if its exit status is
zero, the corresponding __MORE-CONSEQUENT-COMMANDS__ is executed and the command
completes. If else is followed by an __ALTERNATE-CONSEQUENT-COMMANDS__ list, and
the final command in the final if or elif clause has a non-zero exit status,
then __ALTERNATE-CONSEQUENT-COMMANDS__ is executed. The return status is the
exit status of the last command executed, or zero if no condition tested true.

### Examples

```sh
#!/bin/bash
if [ $(whoami) ] != 'root' ] && [ -f "$1" ]; then
    echo "You entered $0 $1, and $1 is a file."
elif [ $(whoami) ] != 'root' ] && [ -d "$1" ]; then
    echo "Error: You entered $0 $1, and $1 is a directory."
else
    echo "Either you are running as root, or your argument was not a file or
    directory."
fi
```
