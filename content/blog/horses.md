---
title: "Multiple horses for multiple courses"
description: "Reliably interfacing programming languages -- thoughts three years on"
date: 2023-07-18T09:00:00+01:00
type: "post"
draft: true
author: "John Lees"
featured_image: '/images/horses.png'
---
This post is about a talk I gave in February 2020 at [RSLondonSouthEast](https://rslondon.ac.uk/rslondonse-2020/),
a local conference for research software engineers. First an overview of the talk, then an update
after following my own advice for the past few years.

# Multiple horses for multiple courses

When deciding which programming language to use for a project, a useful principle
is 'horses for courses' i.e. pick the one that is best suited for the task. How
might you decide which one this is?

- A compiled language? Typically fast to run, but slower to develop.
- An interpreted language? Fast to develop, but slower to run.
- Use the standard language in the field? Usually there's lots of packages available
and also examples. But what if you hate the language?
- Use your favourite language? Development is usually faster and more fun, and you
spend less time on trivial tasks. Sometimes this develops into a semi-religious fervor,
the upshot being that you don't notice the language's disadvantages.

But why compromise? How about using multiple horses for multiple courses? By using
a number of different programming languages for the same project you can:
- Use the dream package. Found some good quality C code that's used everywhere, but haven't written
any C in years? Let's call it from python. Or want to use PyTorch from some C++ code, we can do that too.
- Control over memory and multithreading where you need it. Use a compiled language
just for the pieces that need them.
