---
title: Working with Arrays
keywords: bash, arrays, assignment
last_updated: December 10, 2017
summary: "Arrays are indexed variables that contain multiple values"
toc: true
sidebar: bash_sidebar
permalink: bash_arrays.html
folder: bash
---

## Arrays
* Arrays are indexed variables that contain multiple values.
* Any variable may be used in an array.  
* There's no maximum limit to the size of an array (beyond the memory capacity
     of your machine).
* Arrays are zero-based: the first element in the array is indexed with the
    number zero

## Arrays: Compound assignment
Array variables may be created using compound assignments in this format:

    ARRAY=(value1 value2 ... valueN)

This format is accepted by the *declare* keyword as well.  If no index numbers
are supplied, indexing starts at zero.

### Examples:

The following is an example script we'll call, compound.sh,  that just
 demonstrates a few ways to create arrays in bash, and then output their
 values to stdout (the terminal output).

```sh
#!/bin/bash
myarray=(1 2 3 4 5)
yourarray=( [0]="1" [1]="2" [20]="${myarray[@]}" )
files=(*)

echo ${myarray[@]}
echo ${yourarray[@]}
echo ${files[@]}
```

This script would produce the following output in a bash shell:

    [user@localhost ~]$ bash compound.sh
    1,2,3,4,5
    1 2 1,2,3,4,5
    compound.sh Desktop Documents Downloads Music Pictures Public Templates Videos
    [user@localhost ~]$

## Dereferencing the variables in an array
In order to refer to the content of an item in an array, use curly braces.
 This is necessary, as you can see from the following example, to bypass the
 shell interpretation of expansion operators. If the index number is @ or *,
  all members of an array are referenced.

### Examples:

#### Correct Format

    [user@localhost ~]$ x=(1 2 3)
    [user@localhost ~]$ echo ${x[*]}
    1 2 3
    [user@localhost ~]$ echo ${x[2]}
    3

#### Incorrect Format:

    [user@localhost ~]$ echo $x[*]
    1[*]


Referring to the content of a member variable of an array without providing
 an index number is the same as referring to the content of the first element,
 the one referenced with index number zero.

## Adding Missing or Extra Elements

Adding missing or extra elements in an array is done using the syntax:

    ARRAYNAME[index_number]=value

Remember that the read built-in provides the -a option, which allows for reading
 and assigning values for member variables of an array.

### Example:

    [user@localhost ~]$ myarray=(1 2 3)
    [user@localhost ~]$ echo ${myarray[*]}
    1 2 3
    [user@localhost ~]$ myarray[3]=4
    [user@localhost ~]$ echo ${myarray[*]}
    1 2 3 4

Recall that an array index begins at 0 (**not 1**).

## Indirect Declaration

Indirect declaration is done using the following syntax to declare a variable:

    ARRAY[INDEX]=value

The INDEX is treated as an arithmetic expression that must evaluate to a
positive number.

### Example:

Given an example script we'll call, _declaration.sh_:

```sh
#!/bin/bash
i=5-5
myarray[i]="First"
myarray[1]="Second"

echo ${myarray[@]}
```
Note that we've set a variable, _i_, to the expression _5 - 5_ (which evaluates
    to 0).

This should produce the following output in the bash shell:

    [user@localhost ~]$ bash declaration.sh
    First Second


## Explicit Declaration

Explicit declaration of an array is done using the declare built-in:

    declare -a ARRAYNAME

A declaration with an index number will also be accepted, but the index number
 will be ignored. Attributes to the array may be specified using the declare and
 readonly built-ins. Attributes apply to all variables in the array; you can't
 have mixed arrays.

### Example:

This script we'll call _explicit_declaration.sh_:

```sh
#!/bin/bash
declare -a myarray( "First" "Second")

echo ${myarray[@]}
```

The output for this script should be as follows in a bash shell

    [user@localhost ~]$ bash explicit_declaration.sh
    First Second
    [user@localhost ~]$

## Reading arbitrary values to an array

The Linux cat utility used in the script below, when used without arguments,
 reads from stdin and writes to stdout.

### Examples:

#### Example 1: Reading command-line arguments
```sh
#!/bin/bash
myarray=( $@ )
echo ${myarray[@]}
```

This script can be used from a bash shell like so:

    [user@localhost ~]$ bash read_array.sh 1 2 3
    1 2 3
    [user@localhost ~]$

#### Example 1: Using the _cat_ utility to accept piped input
```sh
#!/bin/bash
# Allow arbitrary elements to be piped into myarray from another script or the
# command-line.
myarray=$( (cat) )
echo ${myarray[@]}
```

This script can be used from a bash shell like so:

    [user@localhost ~]$ echo "1 2 3" | bash read_array.sh
    1 2 3
    [user@localhost ~]$



*Note:* This is potentially unsafe - ensure that any arbitrary input you accept
in your script is properly validated before using it.

{% include links.html %}

## Deleting Array Variables

The unset built-in is used to destroy arrays or member variables of an array

### Examples:

    [user@localhost ~]$ x=(1 2 3 4)
    [user@localhost ~]$ echo ${x[*]}
    1 2 3 4
    [user@localhost ~]$ unset x[1]
    [user@localhost ~]$ echo ${x[*]}
    1 3 4
    [user@localhost ~]$ unset x
    [user@localhost ~]$ echo ${x[*]}

    [user@localhost ~]$
