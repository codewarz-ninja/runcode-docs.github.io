---
title: Working with Variables in BASH
keywords: bash, variables, assignment
last_updated: December 10, 2017
summary: "Variables store data in memory for access at a later time"
toc: true
sidebar: bash_sidebar
permalink: bash_variables.html
folder: bash
---

## Generic Variables
Like any language, variables allow you to store data temporarily in memory and
reference it later in your script.

### Variable assignment

Assignment is as follows:

```sh
#!/bin/bash
x=5
```

### Variable Substitution
The name of a variable is a placeholder for its value, the data it holds.
Referencing (retrieving) its value is called variable substitution.

There are two ways to reference a bash variable:

1) Simplified notation:

```sh
$x
```

2) Standard notation:

```sh
${x}
```

If you try to output the variable x without using variable substitution, you'll
simply output the name of the variable.

### Length of Variables
Bash has a simple method of allowing you to get the length of a variable. For
example, it provides the number of characters in a string, or the number of
indices in an array.

If x is the name of my variable, the syntax for **length of a string** is:

```sh
${#x}
```

If y is the name of an array variable, the syntax for **array length** is:

```sh
${#y[*]}
```

## Constants
Constants are created by making a variable read-only.  The readonly built-in
keyword marks each specified variable as unchangeable.

The syntax is as follows:

    readonly OPTION VARIABLE(s)

Example:

    readonly HELLOWORLD='Hello, World!'

Again, once a readonly variable is assigned a value, it cannot be changed.

## Using the declare built-in

The syntax for declare is the following:

    declare OPTION(s) VARIABLE=value

| Option | Meaning |
|-------|--------|
| -a | declare an array type |
| -f | Use function names only |
| -i | Treat the variable as an integer; arithmetic evaluation is performed when the variable is assigned a value |
| -p | Display the attributes and values of each variable.  When –p is used, additional options are ignored. |
| -r | Make this variable read-only.  These variables cannot then be assigned values by subsequent assignment statements, and they cannot be unset. |
| -t | Gives each variable the trace attribute |
| -x | Mark each variable for export to subsequent commands via the environment. |

Using + instead of - turns off the attribute instead. When used in a function,
declare creates local variables.

### Examples

  TODO

{% include links.html %}
