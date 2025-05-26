---
layout: post
title: Java Command Line Arguments
date: 2018-10-23 16:00:27.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Java
tags:
- java
- oop
- programming
author:
  display_name: deparkes
permalink: "/2018/10/23/java-command-line-arguments/"
---
If you have used other languages, you will probably be familiar with the idea of passing arguments to a program via the command line. This post shows you how you can do it with java.

In this post we'll use a simple script to also take arguments from the command line. Read more about <a href="{{site.baseurl}}/2018/10/16/simple-java-example/">getting started with Java</a>.
This is a file called JavaCommandLineInput.java

```java
public class JavaCommandLineInput {
    public static void main (String[] args) {
        for (String arg : args) {
            System.out.println("Hello, " + arg + "!");
      }
    }
}
```

Much of this code is the same as in this <a href="{{site.baseurl}}/2018/10/16/simple-java-example/">simple Java example</a>, but there are some other elements worth describing here.
<h2>'String[] args'</h2>
The argument to the main method of the JavaCommandLineInput method is '<a href="https://stackoverflow.com/questions/890966/what-is-string-args-parameter-in-main-method-java">String[] args</a>'. This provides a variable which contains any command line arguments provided when the compiled program is run. <a href="https://www.quora.com/Why-is-String-args-compulsory-in-main-method-in-Java">Java is designed for this 'String[] args' argument to be compulsory</a>, so you will need to include it in your programs, even if you do not intend to provide arguments at the command line.

The variable does not need to be called 'args' - it can be anything you want - although it is a strong convention for it to be 'args'. It is <a href="https://stackoverflow.com/questions/5997235/is-there-a-difference-between-mainstring-args-and-mainstring-args">also possible (and equivalent) to write 'String args[]</a>' rather than 'String[] args' and is a matter of choice and coding style as to which one you use.
<h2>Using the Command Line Arguments</h2>
Now that we know we can use the 'args' variable for command line arguments, it is a question of actually doing so. The 'args' variable is an array of strings (which makes sense as any values come directly typed from the command line). In the above example a <a href="https://docs.oracle.com/javase/1.5.0/docs/guide/language/foreach.html">'for-each' loop</a> loops through each of the values in 'args' and print it to the console with println().
<h2>Compile and Run the Code</h2>
Compile this code with

```
javac JavaCommandLineInput.java
```

You can then run this program with:

```
java JavaCommandLineInput Everybody
```

Which gives the output:

```
Hello, Everybody!
```
