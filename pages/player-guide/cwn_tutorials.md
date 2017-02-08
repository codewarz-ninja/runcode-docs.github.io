---
title: The Tutorial Challenges
keywords: sample
summary: "Before climbing the leaderboard, learn about the shebang and command-line arguments."
sidebar: cwn_sidebar
permalink: cwn_tutorials.html
folder: player-guide
---

# Solve These First

The tutorial challenges are there to show new players how their submissions need
to be formatted prior to posting them to the site.  Prior to trying the other
challenges on the site, we recommend you solve the Tutorial challenges first to
set you up for success as you progress further.

## Hello World

This has long been the first program any guide on programming uses to demonstrate
the language.  In Codewarz, we have you submit this first to verify you understand
the format that your submissions need to be in (and that you have a basic functional
proficiency in your language.)

### Interpreted (Scripting) Languages Must Include a Shebang
The shebang is an interpreter directive to a program loader that directs what
interpreter program should be used to parse the rest of the script that follows.

For example, `#!/bin/sh` at the top of a shell script would indicate that `/bin/sh`
should be used to interpret what follows.

The following examples demonstrate the correct way to submit a script for the
languages we support:

#### Bourn-Again Shell (BASH 4.3.46)

hello_world.sh:
{% highlight bash %}
#!/bin/bash
echo "Hello, World!"
{% endhighlight %}

#### Common Lisp

hello_world.lsp:
{% highlight common-lisp %}
#!/usr/bin/env clisp
(print "Hello World")
{% endhighlight %}

#### Nodejs

hello_world.js:
{% highlight js %}
#!/usr/bin/env nodejs
console.log("Hello, World!");
{% endhighlight %}

#### Perl 5 (5.22.1)

hello_world.pl:
{% highlight perl %}
#!/usr/bin/env perl
use strict;
use warnings;
print "Hello, World!\n";
{% endhighlight %}

#### PHP (7.0.8)

hello_world.php:
{% highlight php %}
#!/usr/bin/php
<?php
echo "Hello, World!"
?>
{% endhighlight %}

#### Python (2.7.12)

hello_world.py:
{% highlight python %}
#!/usr/bin/env python
print "Hello, World!"
{% endhighlight %}

#### Python 3 (3.5.2)

hello_world.py:
{% highlight python %}
#!/usr/bin/env python3
print("Hello, World!")
{% endhighlight %}

#### Ruby

hello_world.rb:
{% highlight ruby %}
#!/usr/bin/env ruby
puts "Hello, World!"
{% endhighlight %}

hello_world_object_oriented.rb:
{% highlight ruby %}
#!/usr/bin/env ruby
class HelloWorld
   def initialize(name)
      @name = name.capitalize
   end
   def sayHi
      puts "Hello, #{@name}!"
   end
end

hello = HelloWorld.new("World")
hello.sayHi
{% endhighlight %}

#### Scala

hello_world.scala:
{% highlight scala %}
#!/usr/bin/env scala
object HelloWorld {
  def main(args: Array[String]): Unit = {
    println("Hello, World!")
  }
}
{% endhighlight %}

### Compiled Language Submissions Must be Source Code (No Binaries)

Since compiled languages can't be executed before being compiled (and because
there is no interpreter involved), the shebang line is unnecessary.  Instead,
you can simply submit the source code for your solutions.  They will be compiled
and validated once they are received.

The following are examples of correct Hello World submissions for the compiled
languages that we support:

#### C

hello_world.c:
{% highlight c %}
#include <stdio.h>

int main()
{
    printf("Hello, World!");
}
{% endhighlight %}

#### C++

hello_world.cpp:
{% highlight c++ %}
#include <iostream>

int main()
{
    std::cout << "Hello, World!";
}
{% endhighlight %}

#### C#

hello_world.cs:
{% highlight c# %}
public class Hello_World
{
    public static void Main()
    {
        System.Console.WriteLine("Hello, World!");
    }
}
{% endhighlight %}

#### Golang

hello_world.go:
{% highlight golang %}
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
{% endhighlight %}

#### Haskell

hello_world.hs:
{% highlight haskell %}
module Main where

main = putStrLn "Hello, World!"
{% endhighlight %}

## Argumentative

Most, if not all, of the challenges you will find on Codewarz require your code
to accept some form of input whose format is described for you in the problem
statement. Thus, in order for you to progress through the challenges, you should
first understand how to accept arguments (parameters) passed to your program from
the command-line.
{% include links.html %}
