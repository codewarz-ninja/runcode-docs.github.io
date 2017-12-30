---
title: Iteration in BASH
tags: [tutorial]
keywords: bash, iteration
last_updated: December 29, 2017
summary: How to execute a set of instructions multiple times
toc: true
sidebar: bash_sidebar
permalink: bash_iteration.html
folder: bash
---

## The *for* Loop

### Old-School for loop
This format is reccomended for BASH versions prior to v3.0.  This format uses
a built-in utility called *seq* that simply prints out a sequence of numbers -
effectively building an array (for more information, check out the man page at
[man 1 seq](https://www.freebsd.org/cgi/man.cgi?query=seq&manpath=FreeBSD+9.0-RELEASE)).

#### Format

>for COUNTER in `seq START STOP`<br />
do<br />
&nbsp;&nbsp;COMMAND-LIST<br />
done<br />

#### Example

```sh
#!/bin/bash
for index in `seq 0 5`
do
    echo "This is iteration $i";
done
```

### for loop in range
This format is reccomended as of BASH v3.x+

#### Format

>for COUNTER in {START..STOP}<br />
do<br />
&nbsp;&nbsp;COMMAND-LIST<br />
done<br />

#### Example

```sh
#!/bin/bash

for i in {0..5}
do
    echo "This is iteration $i";
done
```

### for loop over an array

#### Format
> for INDEX in ARRAY<br />
do<br />
&nbsp;&nbsp;COMMAND-LIST<br />
done<br />

#### Example
```sh
#!/bin/bash
for filename in $( ls )
do
    echo -n $filename" "
done
```

### The Three-Expression *for* Loop
This loop syntax is characterized by a three-parameter loop control expression:
the initializer (EXP1), a loop-test or condition (EXP2), and a counting expression
(EXP3).

#### Format
> for (( EXP1; EXP2; EXP3 ))<br />
do<br />
&nbsp;&nbsp;COMMAND-LIST<br />
done<br />

#### Example

```sh
#!/bin/bash
for (( i=0; i<=5; i++ ))
do
    echo "This is iteration $i";
done
```

### Infinite *for* Loops

#### Format
> for (( ; ; ))<br />
do<br />
&nbsp;&nbsp;COMMAND-LIST<br />
done<br />

#### Example

```sh
#!/bin/bash
for (( ; ; ))
do
  echo "This iteration will never end [ hit CTRL+C to stop ]"
done
```

## The *while* loop

### Description
The while construct allows for repetitive execution of a list of commands, as
long as the command controlling the while loop executes successfully (exit
status of zero). 

CONTROL-COMMAND can be any command(s) that can exit with a success or failure
status. The CONSEQUENT-COMMANDS can be any program, script or shell construct.

As soon as the CONTROL-COMMAND fails, the loop exits. In a script, the command
following the done statement is executed.

The return status is the exit status of the last CONSEQUENT-COMMANDS command, or
 zero if none was executed.

### Format
>while CONTROL-COMMAND; do CONSEQUENT-COMMANDS; done

### Example
while_loop.sh:

```sh
#!/bin/bash
# this script will use a while loop to build an array of values
declare -a mylist
declare -i x=1
while [ $x -lt 20 ]
do
    mylist[x]=$x
    x=$((x+1))
done
echo ${mylist[*]}
```

Output:

```sh
[user@localhost ~]$ bash while_loop.sh
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19
[user@localhost ~]$
```

### The infinite *while* loop

#### Format
>while :; do COMMAND; done

#### Example

infinite_while_loop.sh:

```sh
#!/bin/bash
while :
do
    echo "infinite loop [ hit  CTRL+C to stop ]"
done
```

## The *until* loop

### Format

>until TEST-COMMANDS; do CONSEQUENT-COMMANDS; done

### Example

```sh
#!/bin/bash
if [ $# -eq 0 ]; then # $# contains the count of arguments supplied to the script
    echo "No arguments supplied."
    exit 1
fi
until ! read line; do
    echo "$line"
done <"$1"
```
In the example above, the *read* built-in controls the loop.  The script will loop over
each line of a file until there are no more lines in the file. Argument 1 to the
script, $1, is a filename supplied to the loop for read to process.

```sh
#!/bin/bash
COUNTER=20
until [  $COUNTER -lt 10 ]; do
    echo COUNTER $COUNTER
    let COUNTER-=1
done
```
In the example above, the value of COUNTER controls the loop which will iterate
until COUNTER is less than 10.  At each iteration, the loop will print out the
current value of COUNTER to stdout and then decrement the value by 1.

## The *select* loop

### Format
>select WORD [in LIST]; do RESPECTIVE-COMMANDS; done

### Example

```sh
#!/bin/bash

echo "This script will make any of the files in this directory private."
echo "Enter the number of the file you want to protect:"

PS3="Your choice: "
QUIT="Quit the program."
touch $QUIT

select FILENAME in *;
do
    case $FILENAME in
        "$QUIT")
        echo "Exiting."
        break
        ;;
        *)
        echo "You picked up $FILENAME ($REPLY)"
        chmod go-rwx "$FILENAME"
        ;;
    esac
done
rm "$QUIT"
```
LIST is expanded, generating a list of items. The expansion is printed to standard
error; each item is preceded by a number. If in LIST is not present, the positional
parameters are printed, as if in $@ would have been specified. LIST is only printed once.

Upon printing all the items, the PS3 prompt is printed and one line from standard
input is read. If this line consists of a number corresponding to one of the items,
the value of WORD is set to the name of that item. If the line is empty, the items
and the PS3 prompt are displayed again. If an EOF(End Of File) character is read,
the loop exits. Since most users don't have a clue which key combination is used
for the EOF sequence, it is more user-friendly to have a break command as one of
the items. Any other value of the read line will set WORD to be a null string.

The read line is saved in the REPLY variable.

The RESPECTIVE-COMMANDS are executed after each selection until the number
representing the break is read. This exits the loop.

## The *shift* statement

### Description
Shifts the positional parameters of a script to the left by N, where positional
parameters are $1, $2, $3, etc…  If N is not specified, it will default to 1.

Purpose: looping through unknown # of arguments in a script

### Format
>shift [n]

### Example
Given 5 arguments to a script, if N is 2, $3 becomes $1, $4 becomes $2, and
$5 becomes $3.  The original $1 and $2 arguments are unset.

shift.sh:

```sh
#!/bin/bash
# shift.sh

# This script will count the number of files in 1 to many directories

USAGE="Usage: $0 directory1 directory2 directory3 ... directoryN"

if [ "$#" == "0" ]; then
    echo "$USAGE"
    exit 1
fi

while (( "$#" )); do

    if [[ $( ls "$1") == "" ]]; then
        echo "$1 is an empty directory, nothing to be done."
    else
        echo "$1 has $(ls -p $1 | grep -v  / |  wc -l ) files."
    fi

    shift

done
```

The  positional  parameters  from n+1 ... are renamed to $1 ....  Parameters
represented by the numbers $# down to $#-n+1 are unset.  n must be a non-negative
number less than or equal to $#.

If n is 0, no parameters are changed.  If n is not given, it is assumed to be 1.
If n is greater than $#, the positional parameters are not changed.  The return
status is greater than zero if n is greater than $# or less than zero; otherwise 0.

__Output__:

```sh
[user@localhost ~]$ bash shift.sh Downloads/ Documents/ Music/ Desktop/
Downloads/ has 6 files.
Documents/ has 9 files.
Music/ is an empty directory, nothing to be done.
Desktop/ is an empty directory, nothing to be done.
[user@localhost ~]$
```

## Conditional Exit from a loop with the break keyword

### Description
Exit from within a for, while, until, or select loop.  If n is specified, break n levels.  n must be ≥ 1.  If n is greater
than  the  number  of enclosing loops, all enclosing loops are exited.  The return value is non-zero when n is ≤ 0; Other‐
wise, break returns 0 value.

### Format
>break [n]

### Example

#### Example 1

```sh
#!/bin/bash
for (( c = 25; c > 0; c-- )); do
    if [ "$c" -eq 12 ]; then
        echo "Stopping at iteration $c"
        break;
    else
        echo "This is iteration $c"
    fi
done
```

#### Example 2

```sh
#!/bin/bash
# Loop over all files with .sh extension in the current directory
font_red="\033[0;31m"
NC="\033[0;0m"
for file in *.sh
do
    if [ $file == "nested_if.sh" ]; then
        echo -e "${font_red}Skipping $file${NC}"
    else
        # The -L flag will return files that do NOT match
        grep -L 'for' "$file"
    fi
done
```

## Skipping an Iteration with the continue keyword

### Description
The continue statement will resume the script at the next iteration of a for, while,
Until, or select loop.  Nothing following the continue statement will be executed at
the current iteration.

### Format
> continue

### Example

```sh
#!/bin/bash
for (( c = 15; c > 0; c-- )); do
    if [ "$c" -eq 12]; then
        continue
    fi
    echo "This is iteration $c"
done
```

## Exercises

1. Use for loops to display only odd numbers from 1 to 99 (one number per line).
2. Use a while loop to display only even numbers from 1 to 99 (one number per line).
3. Use any loop to display all numbers from 1 to 50 in reverse order.
