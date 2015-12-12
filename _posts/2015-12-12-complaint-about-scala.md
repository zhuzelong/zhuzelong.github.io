---
layout:
title: Complaint about Scala and Reviews
categories: []
tags: [scala]
published: True

---
I am learning Scala, the so-called "OO + FP" language. It is said that Scala is the only language that is more complicated than C++. I know little about C++ or any FP language but I found Scala really complicated, or "disorder".

I decided to set up a post to keep track of my learning Scala. This post will be about complaint, i.e. the points that I found Scala "unreasonable" or "confusing". More importantly, I would like to review these complaint and try to find out whether I am wrong.

I have background of Python and Java, though not an advanced programmer. So the following "complaints" would be based comparison between Scala and Python/Java.


## Symbol

Scala is said to "save the time of programmer" and "concise" compared with Java. So why do I have to type so many "shift" to spell the symbol `<-`, `=>`. Java is indeed verbose but it is definitely easy to read. We probably found Java too loooong to read but we can certainly understand the statements without much "compilation". By contrast, Scala is short and concise, but is it easy to read? Is `filter(map)` or a method invoked without `()` friendly to the readers? I assert that the "non-genius" programmers would have to think and "compile" when they read Scala code.

Scala is absolutely easy to write, but not so easy to read. Scala can compress the code but not the information underlying the code. Moreover, I believe that code is more often for reading instead of writing.


## I/O and Serialize

I love the Python I/O and pickle module so much because I can read or write anything in a few (usually 2-3 lines) statements which are easy to read. The `with open() as` syntactic sugar is so much lovely that I can get rid of the `close()` statement. When it comes to Scala, wait a minute, there is no core I/O and serde package in Scala? There was one in Scala 2.9 and then deprecated. What should I refer to then? Java libraries. In short, I/O and serde are such necessary and basic functionalities that I believe the core package should include them. If I have to refer to Java libs for such basic functionalities, why would I need Scala? Once again, we may be able to compress the code (recall the verbose `XXInputStream, XXOutputStream`) but not information. I am in favor of Python I/O and serde.
