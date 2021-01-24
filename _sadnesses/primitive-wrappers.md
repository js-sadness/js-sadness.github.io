---
layout: sadness
title: "0 is a number, not a Number"
description: "Each primitive type also has an additional class with that name"
resolved: false
# published: false

categories: 
    - "typing"
---

## The Facts

The [primitive types](https://developer.mozilla.org/en-US/docs/Glossary/Primitive) 
should not be confused with the 
[fundamental types](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects),
which are built-in classes like `Object`, `String` or `Number`.
These prototypes are wrapper types which can be constructed 
using a _real_ number or a _real_ string.

Even though strings don't inherit from `String`,
JavaScript automatically wraps strings into a `String` where required,
such that all of `String`s methods can be called on a string.
Sounds like inheritance at first, but is not.

> Fun fact: Object literals do inherit from the `Object` wrapper class.

See [this sadness to learn more about `instanceof` and `typeof`](/sadnesses/instanceof-typeof).

## Why is this a Problem

Primitive objects possessing all the functionality
of their wrapper types suggests that they inherit from them, 
which they don't. To write correct JavaScript, it is sometimes 
required to know this implementation detail of the language.

## Our Suggestion to improving the language

Wrapper types should not be necessary. 
Primitive types should be an implementation detail
which the programmer should not need to bother with.
Just put the `split` method on the real string 
instead of automatically wrapping it!  

Getting rid of the distiction between primitive and wrapper types
also frees us from having two different functions for checking the type: 
`instanceof` and `typeof` would be the same. 
(Find out why they are not the same in [this sadness](/sadnesses/instanceof-typeof).)

## Workarounds that work today

There's nothing we can do.
