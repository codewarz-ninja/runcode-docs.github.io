---
title: Grabbing User Input
tags: [tutorial]
keywords: bash, input
last_updated: December 29, 2017
summary: Making your shell scripts interactive
toc: true
sidebar: bash_sidebar
permalink: bash_input.html
folder: bash
---

## Script Arguments

### Description
BASH allows you to access arguments passed to your script using *positional
parameters*.  These work just like variables except that their names are numbers
that correspond to the order an argument was passed to the script.

For example, $0 is the name of the script, $1 is the first argument passed to
the script, $2 is the second argument, and so on.

Positional parameters are used in place of what other languages like C refer to
as the argument vector (passed to the main function as char argv[] ).

### Format

>$0 $1 $2 $3

### Examples

```sh
#!/bin/bash
#Print all arguments to the script
echo $@

#Print the name of the script
echo $0

#Print the first argument to the script
echo $1

#Print the number of arguments passed to the script
echo $#
```

## The *read* built-in

### Format

>read [options] *variable*

### Examples

```sh
#!/bin/bash
# This script demonstrates the use of the BASH read built-in
read username
echo "$username"

# Only read n characters
read -n 1 value
echo "$value"

# Read with a prompt
read -p "Please enter your name: " name
echo "$name"
```

## Exercises

1. Write a script that will prompt the user for a filename and print it to stdout (standard out).
2. Write a script that reads only the first two characters of user input.
3. Write a script that will prompt the user and accept input in the same command.
