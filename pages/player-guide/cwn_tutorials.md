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

Argumentative asks you to print all of the arguments to
your app from the command-line.  This challenge does not
provide you with the number of arguments you should expect.
Instead, your solution should be able to print one-to-many
arguments to the screen.

For example, in the shell script below, there are four
arguments provided at the command-line.

```bash
$ ./your_app.sh one two three four
```

The solution, should provide all four arguments not including argument 0 (the app name itself).

```bash
$ ./your_app.sh one two three four
one two three four
```

Below are the solutions you should be able to provide to this tutorial challenge in any of the 14 languages you are
using.

#### Bourn-Again Shell (BASH 4.3.46)

argumentative.sh:
{% highlight bash %}
#!/bin/bash
echo $@
{% endhighlight %}

#### Common Lisp

argumentative.lsp:
{% highlight common-lisp %}
#!/usr/bin/env clisp
(loop for i in *args*
    do (format t " ")
    do (format t "~A" i)
    )
{% endhighlight %}

#### Nodejs

argumentative.js:
{% highlight js %}
#!/usr/bin/env nodejs
process.argv.slice(2).forEach(function (val, index, array) {
    process.stdout.write(val+" ");
});
console.log();
{% endhighlight %}

#### Perl 5 (5.22.1)

argumentative.pl:
{% highlight perl %}
#!/usr/bin/env perl
use strict;
use warnings;
print "$_ " foreach @ARGV;
print "\n"
{% endhighlight %}

#### PHP (7.0.8)

argumentative.php:
{% highlight php %}
#!/usr/bin/php
<?php
for($i = 1; $i < sizeof($argv); $i++) {
    echo $argv[$i]." ";
}
echo "\n";
?>
{% endhighlight %}

#### Python (2.7.12)

argumentative.py:
{% highlight python %}
#!/usr/bin/env python
import sys
print ' '.join(sys.argv[1:])
{% endhighlight %}

#### Python 3 (3.5.2)

argumentative3.py:
{% highlight python %}
#!/usr/bin/env python3
import sys
print(' '.join(sys.argv[1:]))
{% endhighlight %}

#### Ruby

argumentative.rb:
{% highlight ruby %}
#!/usr/bin/env ruby
puts ARGV.join(' ')
{% endhighlight %}

#### Scala

argumentative.scala:
{% highlight scala %}
#!/usr/bin/env scala
object Argumentative {
  def main(args: Array[String]): Unit = {
      println(args.mkString(" "))
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

argumentative.c:
{% highlight c %}
#include <stdio.h>

int main(int argc, char *argv[])
{
    int i = 0;
    for(i = 1; i < argc; i++) {
        printf("%s ", argv[i]);
    }
    printf("\n");
}
{% endhighlight %}

#### C++

argumentative.cpp:
{% highlight c++ %}
#include <iostream>

int main(int argc, char *argv[])
{
    int i = 0;
    for(i = 1; i < argc; i++) {
        std::cout << argv[i] << " ";
    }
    std::cout << std::endl;
}
{% endhighlight %}

#### C#

argumentative.cs:
{% highlight c# %}
using System;
public class Argumentative
{
    public static void Main(string[] args)
    {
        for (int i = 0; i < args.Length; i++)
        {
            System.Console.Write("{0} ",args[i]);
        }
        System.Console.WriteLine();
    }
}
{% endhighlight %}

#### Golang

hello_world.go:
{% highlight golang %}
package main

import "os"
import "fmt"
import "strings"

func main() {
    argsWithoutProg := strings.Join(os.Args[1:], " ")
    fmt.Println(argsWithoutProg)
}
{% endhighlight %}

#### Haskell

hello_world.hs:
{% highlight haskell %}
import System.Environment
import Data.List

main = do
    args <- getArgs
    putStrLn (intercalate " " args)
{% endhighlight %}
{% include links.html %}
