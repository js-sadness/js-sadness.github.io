---
title: "String Types"
description: "Some values are stored as strings but shouldn't be"
why-bad: "Results in unnecessary, error prone parsing and stringifying code."
---

## Strings are not Types

Don't use complex Strings with an implicit syntax
where a plain object could have been used. 
The worst part is that everyone interacting with
it has to parse it or generate a new string everytime.
It's another thing that must be documented
and it circumvents all syntax checks.

Also, checkout the [Type System Category](/categories/typing) for similar sadness.
