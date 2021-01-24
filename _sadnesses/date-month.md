---
layout: sadness
title: "`Date.getDay()` starts at 1"
resolved: false
description: "All `Date` members start at 0, only days start at 1"
published: false
categories:
    - "inconsistent"
    - "browser"
---

## The Facts

The `Date` class contains several methods to extract 
the numerical index of the second, minute, hour, day, month, or year.

All these indices start at 0 – except for the day, which starts at 1.

## Why is this a Problem

<!-- Include all generic reasons for each category that contains this sadness -->
{% include category-reasons.html %}

Inconsistencies require programmiers to keep a special case in mind.
When skimming over the documentation without prior knowledge about Dates,
it may not be obvious that Days are different, thus producing bugs in your code.

## Our Suggestion to improving the language
Every method returning an index should start from the same base - either 1 or 0.

## Workarounds that work today
Keep in mind to add a 1 to every `getDay()` index!
