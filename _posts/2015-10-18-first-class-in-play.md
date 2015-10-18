---
layout: post
title: First class in Play!
categories: [Remarks]
tags: [web]
published: True

---
I spent the last 4 days in learning Play framework by reading the documentation and following the examples. This is the first time when I learn a web framework. I heard about quite a few names of framework but knew little about them.

First thing first, I found Java powerful and comprehensive but I do dislike Java. Java is powerful partly due to the optimization of JVM. When people find Python or similar "script languages" under performance, they usually turn to Java/C++ which seem to be "the final solution". Java is such a verbose and inconsistent language. I am not "afraid" of programming in Java but I find it time consuming and exhausting to write Java code.

Play is a new framework that imitating RoR, Django to be less "Java-style". But I still got loss in the naming convention of Play. The authors of Play thought that developers would appreciate the predefined "naming shortcuts", e.g. put an 's' after a Model's name to be a CRUD controller, reference to the HTML parameters by accessing the identical name directly. But why the argument `as` in a view becomes `_as` in a "tag" (another type of view) without any explanation in the documentation? Why the pages were down when I changed the parameter name `postId` to `id`? The underlying "naming shortcuts" make such a chaos and I think the homepage of Play should offer a complete list of such shortcuts.


Secondly, it took me a few hours to understand the "flow" of MVC. There are a lot of `#{if}` in the views, namely, a logical structure in the views, which I thought should be put in the controllers. The MVC in Play looks like jam (I don't know how MVC in other frameworks looks like).

