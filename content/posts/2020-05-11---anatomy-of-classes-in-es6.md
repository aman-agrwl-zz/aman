---
title: Anatomy of class in ES6
date: "2020-05-10T22:40:32.169Z"
template: "post"
draft: false
slug: "class-in-es6"
category: "JavaScript"
tags:
  - "JavaScript"
  - "ES6"
  - "Web Development"
description: "ES6 Classes formalize the common JavaScript pattern of simulating class-like inheritance hierarchies using functions and prototypes. They are effectively simple sugaring over prototype-based OO, offering a convenient declarative form for class patterns which encourage interoperability."
socialImage: "/media/42-line-bible.jpg"
---


In object-oriented programming, a class is an extensible program-code-template for creating objects, providing initial values for state (member variables) and implementations of behavior (member functions or methods).



## The-syntactical-sugar

Still, there are important differences.

1. First, a function created by class is labelled by a special internal property [[FunctionKind]]:"classConstructor". So it’s not entirely the same as creating it manually.
2. Class methods are non-enumerable. A class definition sets enumerable flag to false for all methods in the "prototype".
3. Classes always use strict. All code inside the class construct is automatically in strict mode.

### static keyword 
