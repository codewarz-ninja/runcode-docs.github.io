---
title: Introduction
keywords: bash, introduction
summary: "Shell-Scripting is a 1950's Jukebox - Larry Wall"
sidebar: bash_sidebar
permalink: bash/introduction.html
folder: bash-tutorial
---

## What is Shell Scripting?

The shell is a command interpreter – examples include bash, csh, ksh, sh. Simply
put, a shell script is a text file that allows you automate or “glue together”
any set of commands/tasks you would normally have to type by hand. In addition
to almost the entire repertoire of Linux commands, utilities, and tools you
could normally invoke from the command-line, a shell script also permits
conditional statements, loops, and testing constructs. Shell scripts are best
suited for administrative tasks, and any routine tasks that don’t require a
full-blown programming language.

## Starting off with a Sha-bang

In Linux and other Unix-Like operating systems, when the first line of a script
contains a #!character sequence, the program loader interprets what follows as a
directive to use that interpreter.

Examples include:

    #!/bin/python
    print “Hello, World!”

    #!/bin/bash
    echo “Hello World!”

    #!/bin/cat
    Hello World!

## Variables
Like any language, variables allow you to store data temporarily in memory and
reference it later in your script.

### Variable assignment

Assignment is as follows:

    #!/bin/bash
    x=5

There are two ways to reference a bash variable:

### Variable Substitution
The name of a variable is a placeholder for its value, the data it holds.
Referencing (retrieving) its value is called variable substitution.

Simplified notation:
    $x

or

Standard notation:

    ${x}

If you try to output the variable x without using variable substitution, you'll
simply output the name of the variable.

### Length of Variables
Bash has a simple method of allowing you to get the length of a variable. For
example, it provides the number of characters in a string, or the number of
indices in an array.

If x is the name of my variable, the syntax for length of a string is:
    ${#x}

If y is the name of an array variable, the syntax for array length is:
    ${#y[*]}

### Constants
Constants are created by making a variable read-only.  The readonly built-in
keyword marks each specified variable as unchangeable.

The syntax is as follows:

    readonly OPTION VARIABLE(s)

Example:

    readonly HELLOWORLD='Hello, World!'

Again, once a readonly variable is assigned a value, it cannot be changed.
