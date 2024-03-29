---
layout: post
comments: true
title:  "CI Lisp"
date:   2016-08-03 18:30:10 -0500
categories: programming
---

Two semesters ago, I wrote a Lisp interpreter in my Programming Language & Design class.
This was one of the most satisfying school projects that I have had the chance to work on.

Looking back on it, I think I could have implemented some things much better - but that is
an opportunity for future work. Here is a summary of some of the features that I was able
to implement.

## Types

There are two types in ciLisp. They are real and integer. Integer is your typical integer
and real behaves as a double. Variables must be initialized and declared with desired
types before they can be used. Variables are coerced with the following rules:

   - Integers should be coerced into reals by adding a zero fraction part. Ex: 1 -> 1.0
   - Reals should be coerced into integer variables by rounding to the closest integer
     (down or up). Ex: 1.49 -> 1 and 1.69 to 2
   - The type of an expression should be integer if only expressions of type integer are
     used to compute it. Otherwise, it should be real.

The evaluated result will be printed as a real number (even if it is an integer), although
the proper coercion takes place.

## Variables

Variables are declared using the let keyword. The scope in which they exist is the
s-expression that immediately follows the let statement. You can create an arbitrary
number of variables within one let statement.

![](assets/cilisp1.png)

## Conditionals

Conditionals are done using the cond keyword with the following syntax: (cond (condition)
(do this if its true) (do this if its false))

The cond function checks to see if the first expression evaluates to true (non-zero). If
so, the second expression is evaluated and returned. Otherwise, the third s_expression is
evaluated and returned. The conditional functions equal, smaller, and larger all return 1
if the condition holds and 0 otherwise.

![](assets/cilisp2.png)

## Standard In and Out

The print function takes an expression and prints it to standard out.

The read function is a parameter-less function that reads a number from standard input and
can be used to assign a variable.

![](assets/cilisp3.png)

## Random Numbers and Math Functions

The rand function is another parameter-less function that is used for generating a random
number. The time of execution is used as the seed for the random number generator.

The standard library includes the following math functions : neg, abs, exp, sqrt, exp2,
cbrt, hypot, add, sub, mult, div, remainder, log, pow, max, min.

![](assets/cilisp4.png)

## Static Scoping

CI-Lisp implements static scoping, which means that it looks for the most recently
declared variable with a given name, then its parent scope, and so on.

The type of a variable is inherited if it was declared in a previous scope. So, in the
below example, myVar did not need to be declared with a type, although it could have.

![](assets/cilisp5.png)

Having had some time to reflect on this project, my next project will be to rewrite this
interpreter in either Rust or Go (wanting to learn both) and improve/expand the feature
set.

As I make progress, I will keep the blog updated!
