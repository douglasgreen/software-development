# Code Libraries vs. Frameworks

"PageMaker" is a library, not a framework. To understand the distinction, it's
crucial to define what libraries and frameworks are and how they function within
software development.

## What is a library?

A library is essentially a collection of pre-written code, which can be
functions, classes, or components, that a programmer can leverage to perform
specific tasks. Instead of rewriting the same code every time, a programmer can
simply call the required function or class from the library. With a library like
PageMaker, you have the autonomy to decide when and where to invoke these
functionalities within your application.

## What is a framework?

In contrast, a framework is a more comprehensive tool that not only offers
libraries but also defines the overarching structure of applications. When you
use a framework, you are provided with a set of rules and guidelines to create
your code. This means that the framework dictates the flow of the application,
and you essentially fill in the gaps with your own code as specified by the
framework.

The core difference between the two revolves around the concept of "inversion of
control". With a library, you (the programmer) maintain control over the
application's flow, deciding when and where to use the library. In the case of a
framework, it is the framework that controls the flow, calling your code when
and where it deems necessary.

## Why is PageMaker a library?

PageMaker qualifies as a library because it primarily offers a collection of
independent components that developers invoke as required. While PageMaker might
provide certain organizational guidelines for code and files, it does not
control or dictate the overall workflow of the program.

<!-- DSG/ChatGPT 7/25/2023 -->
