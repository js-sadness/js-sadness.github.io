---
layout: sadness
title: "`instanceof` disagrees with `typeof`"
description: "`typeof null === 'object'`, but `null instanceof Object === 'false'`"
resolved: false
# published: false

categories: 
    - "typing"
    - "naming"
    - "inconsistent"
---

## The Facts

The operators `typeof` and `instanceof` are not related in any way.
Whereas `typeof` returns one of the primitive type names,
`instanceof` walks the [prototype chain](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain) 
to check whether an object inherits from a prototype.

This seems reasonable at first glance. However, it is not
directly clear which objects have a prototype and which don't.

For example, `typeof null === 'object'` but `null instanceof Object === 'false'`.
This is because `Object` is a function, and not a primitive type.
The value `null` does not have a prototype.
  
Furthermore, `typeof 'text' === 'string'` but `'text' instanceof String === 'false'`,
and `typeof 0 === 'number'` but `0 instanceof Number === 'false'`.
These values also do not have a prototype.

__The catch: `typeof ({x:1}) === 'object'` and `({x:1}) instanceof Object === 'true'`.__ 
So object literals do have the wrapper class `Object` as a prototype.

The primitive types should not be confused with the [fundamental types](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects),
which are built-in prototypes like `Object`, `Boolean` or `Number`.

The fact that there is a difference 
between those primitive and fundamental types
is a problem on its own. You can read more about it
in [this sadness about wrapper types](/sadnesses/primitive-wrappers).

## Why is this a Problem

The operators `instanceof` and `typeof` look very similar, 
but they are not. This may lead to confusion. 
The wording `instanceof` does not communicate that the 
prototype of an object will be inspected, 
and not its primitive type.

Furthermore, primitive objects possessing all the functionality
of their wrapper types suggests that they inherit from them, 
which they don't.

## Our Suggestion to improving the language

The operator `instanceof` should not have been blindly
copied from Java or another language with real classes. 
Instead, it could have been called `hasprototype`.
This could even be a plain function.

Furthermore, `typeof null` could return 
the string `'null'` instead of  `'object'`. 
Any value can be null, because the type system is dynamic 
and the abscence of a value prevents us from finding out its type.

Primitive types should be an implementation detail
which the programmer should not need to bother with.
This would render `instanceof` and `typeof` redundant
and simplify the language.

## Workarounds that work today

Be sure to know everything about [JavaScript Prototypes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/prototype).
They may look like typical classes on first glance, but are certainly not.
