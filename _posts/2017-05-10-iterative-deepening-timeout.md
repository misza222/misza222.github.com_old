---
layout: post
title:  "Iterative deepening and with reliable timeout"
date:   2017-05-10 09:00:00 -0100
categories: ai
---

Use case for [iterative deepening](https://en.wikipedia.org/wiki/Iterative_deepening_depth-first_search) is to return most complete result it is possible within a certain time constraint.

Here is my implementation of the timer and how to handle it in Python. It is Unix specific as it uses BSD signals, and will not work on Windows (but works on Mac of course).

<script src="https://gist.github.com/misza222/93b51e15136e7448b19fb089c3ec51af.js"></script>
