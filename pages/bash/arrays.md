---
title: Working with Arrays in BASH
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
{% include note.html content="
The * character as demonstrated in the assignment to the *files* variable above is
a glob pattern for any string which pathname-expands into all the filenames in
the current directory (just like it would if you typed 'rm *' directly on the
command-line). After the pathname expansion, the command will look like
files=(file1 file2 file3 file4 ...) which assigns all of the files to the array
 files." %}

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

## Appending New Values to an Array

### Examples:

#### Example 1
This is perhaps the safest method of appending to an array.

    [user@localhost ~]$ x=(1 2 3 4)
    [user@localhost ~]$ echo ${x[@]}
    1 2 3 4
    [user@localhost ~]$ x+=(5)
    [user@localhost ~]$ echo ${x[@]}
    1 2 3 4 5
    [user@localhost ~]$

#### Example 2
This method only works for arrays that are _compact_ (contiguous indices).

    [user@localhost ~]$ x=(1 2 3 4)
    [user@localhost ~]$ echo ${x[@]}
    1 2 3 4
    [user@localhost ~]$ x[${#x[@]}]=5
    [user@localhost ~]$ echo ${x[@]}
    1 2 3 4 5

This example above takes advantage of the fact that arrays in bash are 0-indexed;
thus the size of the array will conveniently also be the next open element _if_
the array is compact (no indexes that are out of order).  

For example, consider a case where a value is added to the array at an index
that is clearly not the next available index:

    [user@localhost ~]$ x=(1 2 3 4)
    [user@localhost ~]$ echo ${x[@]}
    1 2 3 4
    [user@localhost ~]$ echo ${#x[@]} # size of array
    4
    [user@localhost ~]$ echo ${!x[@]} # indices in array
    0 1 2 3
    [user@localhost ~]$ x[9999]=5
    [user@localhost ~]$ echo ${x[@]}
    1 2 3 4 5
    [user@localhost ~]$ echo ${#x[@]}
    5
    [user@localhost ~]$ echo ${!x[@]}
    0 1 2 3 9999

As you can see, Example 2 could potentially cause issues if you are not careful.
The shell shown above belies the fact that BASH arrays are _sparse_ which means
that they are not necessarily contiguous indices.

## Getting the Size of the Array
This is almost identical to how you would get the size of a normal variable. The
difference with printing the size of an array is that instead of getting the number
of characters or bytes of the variable, you're going to get a number representing
the number of values in the array.

### Example:

    [user@localhost ~]$ x=(1 2 3 4)
    [user@localhost ~]$ echo ${x[@]}
    1 2 3 4
    [user@localhost ~]$ echo ${#x[@]}
    4

The last line in the example above demonstrates how you print the size of the
array.  Just prefix the variable name with a # symbol.

## Getting all Array Indices

This is useful if you want to create a loop that can print your index and value.

### Examples:

#### Example 1
Simply output all array indices into an unnamed array

    [user@localhost ~]$ x=(1 2 3 4)
    [user@localhost ~]$ echo ${!x[@]}
    0 1 2 3
    [user@localhost ~]$

#### Example 2
Iterate over each index of the array and print the index and value

    [user@localhost ~]$ x=(1 2 3 4)
    [user@localhost ~]$ for i in ${!x[@]}; do echo "Index: $i, Value: ${x[$i]}"; done
    Index: 0, Value: 1
    Index: 1, Value: 2
    Index: 2, Value: 3
    Index: 3, Value: 4
    [user@localhost ~]$

In a script, you might want your loop to be expanded out to a more readable form:

```sh
#!/bin/bash
x=(1 2 3 4)
for i in ${!x[@]}
do
    echo "Index: $i, Value: ${x[$i]}"
done
```

## Deleting Array Variables

The unset built-in is used to destroy arrays or member variables of an array

### Examples:

#### Example 1
Deleting a value from an array using unset.

    [user@localhost ~]$ x=(1 2 3 4)
    [user@localhost ~]$ echo ${x[*]}
    1 2 3 4
    [user@localhost ~]$ echo ${#x[*]}
    4
    [user@localhost ~]$ unset x[1]
    [user@localhost ~]$ echo ${x[*]}
    1 3 4
    [user@localhost ~]$ echo ${#x[*]}
    3
    [user@localhost ~]$ echo ${x[1]}

    [user@localhost ~]$ echo ${x[@]}
    1 3 4

The problem with using unset on an array is that it will leave your array with
a null index for each index that you unset (rather than resetting the index of
the array.)  In order to compact the array, you'll have to use the technique
shown in example 2 below.

#### Example 2
Deleting a value from an array that has no unset elements (until index + 1)

    [user@localhost ~]$ x=(1 2 3 4)
    [user@localhost ~]$ INDEX=1
    [user@localhost ~]$ echo ${x[@]}
    1 2 3 4
    [user@localhost ~]$ echo ${#x[*]}
    4
    [user@localhost ~]$ x=( "${x[@]::$INDEX}" "${x[@]:$((INDEX+1))}" )
    [user@localhost ~]$ echo ${x[@]}
    1 3 4
    [user@localhost ~]$ echo ${#x[@]}
    3
    [user@localhost ~]$ echo ${x[INDEX]}
    3

This method works because it's essentially using array splicing to create an
entirely new array called x that has all but the index you wanted to delete.

#### Example 3
Deleting the array itself

    [user@localhost ~]$ unset x
    [user@localhost ~]$ echo ${x[*]}

    [user@localhost ~]$

## Exercises

1. Display the name of the script being executed
2. Display the first, third, and tenth argument given to the script
3. Display the total number of arguments passed to the script

{% include links.html %}
