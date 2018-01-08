---
title: BASH by Example
tags: [tutorial]
keywords: bash, variables, assignment, introduction
last_updated: December 10, 2017
summary: "Shell-Scripting is a 1950's Jukebox - Larry Wall"
toc: true
sidebar: bash_sidebar
permalink: bash_introduction.html
folder: bash
---

# Introduction

This tutorial was started because there are not many guides out there that teach
bash scripting by example.  This will be a work in progress, and more content
will be added as time permits.

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

```sh
#!/bin/sh
print “Hello, World!”
```

```sh
#!/bin/bash
echo “Hello World!”
```

```sh
#!/bin/cat
Hello World!
```

## Exercises

1) Submit the [Hello_World](https://codewarz.ninja/do_challenge/Hello_World) tutorial challenge.
