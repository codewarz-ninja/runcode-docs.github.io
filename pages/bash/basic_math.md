---
title: Basic Math in BASH
tags: [tutorial]
keywords: bash, math
last_updated: January 8, 2017
summary: "Addition, Subtraction, Multiplication, and Division in the Shell"
toc: true
sidebar: bash_sidebar
permalink: bash_basic_math.html
folder: bash
---

# Introduction

BASH was not designed to do anything but the most basic math operations, and
does not natively support anything more than integer operations.  However, there
are a few shell utilities that can overcome this limitation (namely _bc_).

## Arithmetic Evaluation

### Description
This command evaluates a given arithmetic expression, _&lt;EXPRESSION&gt;_.

Arithmetic evaluation implements the standard PEMDAS order of operations (Parentheses,
Exponents, Multiplication, Division, Addition, Subtraction).

It does _not_ support arithmetic operations on floating-point numbers (only
integer values are supported).

### Format
>(( &lt;EXPRESSION&gt; ))

### Examples

    $ echo $(( 5+5 ))
    10
    $ echo $(( 5*5 ))
    25
    $ echo $(( 5/5 ))
    1
    $ echo $(( 5-5 ))
    0
    $ echo $(( 12 * 13 ))
    156
    $ echo $(( 5+6/3*2 ))
    9
    $ echo $(( (5+6)/3*2 ))
    6
    $ echo $(( 5 % 5 )) # modulus (divides and returns remainder)
    0
    $ echo $(( 5 % 6 ))
    5
    $ echo $(( 2**16 ))
    65536
    $

## The let built-in

### Description
This command is similar to the arithmetic evaluation command, except that it
is specifically designed to set variables to the result of a given expression (
as opposed to direct output of the result).

This command implements the standard PEMDAS order of operations (Parentheses,
Exponents, Multiplication, Division, Addition, Subtraction).

It does _not_ support arithmetic operations on floating-point numbers (only
integer values are supported).

### Format
>let x=<EXPRESSION>

### Examples

    $ let a=5+5
    $ echo $a
    10
    $ let a=5*5
    $ echo $a
    25
    $ let a=5/5
    $ echo $a
    1
    $ let a=5-5
    $ echo $a
    0
    $ let b=5+6/3*2
    9
    $ let b=(5+6)/3*2
    6
    $ let a=5%5 # modulus (divides and returns remainder)
    $ echo $a
    0
    $ let a=5%6
    $ echo $a
    5
    $ let a=2**16
    $ echo $a
    65536
    $

## bc (basic calculator) - an arbitrary precision calculator language

### Description
_bc_ is a built-in shell utility that interprets an "interactive algebraic language
with arbitrary precision" by the same name.  While there is a lot it can do, it
would be outside the scope of this tutorial to explain it all.

The primary advantage to using _bc_ for solving challenges on the site is that
it __natively handles floating-point operations__ (not just integers).

We'll just cover the basics here.  For more information, you can read the manual
on the GNU website here: [bc](https://www.gnu.org/software/bc/manual/html_mono/bc.html).

### Format
>echo &lt;EXPRESSION&gt; &#124; bc

While bc can be used in many more ways than simply piping expressions into it,
this is a simple format that is easy to understand for basic calculations.

### Examples

    $ echo 5.5 + 5.6 | bc
    11.1
    $ echo 5.5 % 5.5 | bc
    0
    $ echo 5.5 % 5.6 | bc
    5.5
    $ echo 2^16 | bc
    65536

## Exercises

1. Submit [Simple_Addition](https://codewarz.ninja/do_challenge/Simple_addition) (10 point challenge)
2. Submit [Stupid_Addition](https://codewarz.ninja/do_challenge/Stupid_addition) (10 point challenge)
3. Submit [Summation_as_a_service](https://codewarz.ninja/do_challenge/Summation_as_a_service) (10 point challenge)
4. Submit [Strange_Addition](https://codewarz.ninja/do_challenge/Strange_addition) (12 point challenge)
5. Submit [Adding_Horizontally](https://codewarz.ninja/do_challenge/Adding_Horizontally) (15 point challenge)
6. Submit [Quad_Math](https://codewarz.ninja/do_challenge/Quad_math) (15 point challenge)
7. Submit [Multiplicity](https://codewarz.ninja/do_challenge/Multiplicity) (15 point challenge)
8. Submit [Range_Multiplication](https://codewarz.ninja/do_challenge/Range_Multiplication) (15 point challenge)
9. Submit [Evenly_Divisible](https://codewarz.ninja/do_challenge/Evenly_Divisible) (10 point challenge; what is a number?)
