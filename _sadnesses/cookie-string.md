---
layout: sadness
title: "Cookies are a String"
resolved: false
description: "Cookies should be an array getter and setter, not a String containing all elements"

categories: 
    - "strings"
    - "browser"
    
published: false
---

## The Facts

The [property `document.cookie` is defined](https://developer.mozilla.org/en-US/docs/Web/API/Document/cookie) 
to store a specific string:
- Setting its value will append a single cookie to the session. 
- Getting its value however will return all cookies joined to a single string. 
  The syntax can best be described using an example:
  ```
  cookie1Name=value1; cookie2Name=value2
  ```

## Why is this a Problem

<!-- Include all generic reasons for each category that contains this sadness -->
{% include category-reasons.html %}

A variable always returning something different 
than what you put into it is not what variables are intended for.  

Also, returning a string containing a joined list requries the
programmer to manually lookup the syntax definition and come up with a parsing algorithm.

Cookies are an essential part of the web and thus should be easy to use.

## Our Suggestion to improve the language
A better design would be to offer a pair of functions called   
`putCookie(name, { value, expires, ... })` and  
`getCookies(): { name: { value, expires, ... }, ... }`.   
Accessing data using a getter function 
implies that the data may change, 
which happens to be the case for cookies, 
since they are removed as soon as they expire.

Also, those functions returning the cookies as a map containing key/value pairs, 
but not a single string which must be parsed manually every time,
would increase ergonomy greatly.

## Workarounds that work today
As always, npm is here to save us. 
There are many libraries written to increase the ergonomy of handling cookies.


Alternatively, you can use the following snippets to handle cookies:
```javascript
putCookie = (name, data) => 
    document.cookie = `${name}=${data.value};` + 
        `expires=${data.expires};secure`

getCookies = () => Object.fromEntries(
    (document.cookie || '').split('; ')
        .map(entry => entry.split('='))
)

```


<!-- 
Accessing cookies is a breeze if you're using JavaScript. 
Cookies are a collection of named objects, 
much like a regular object having multiple named properties.
Conveniently, the browser puts all cookies into a string for 
us so that we don't have to join them manually.
```javascript
console.log(document.cookie)
// prints 'name1=value1; name2=value2' for our two cookies
```
In the rare case that you want to inspect only a single cookie
and not all of them at once, you only have to parse that string 
according to a common format consisting of semicolons.
```javascript
console.log(Object.fromEntries((document.cookie || '').split('; ').map(entry => entry.split('=')))
// prints { name1: 'value1', name2: 'value2' } for our two cookies
```


Now, inserting a cookie is easier than you might think.
Contrary to our first example, luckily, we don't have to search and replace our cookies in `document.cookie`. 
Instead, we only need to provide the value for the cookie we want to update.
Fortunately, we can pass a string directly from our user input 
and we don't have to parse it from a string to a silly object first.
```javascript
document.cookie = 'name=value;expires=Wed, 20 Nov 2019 23:34:57 GMT;secure'
```
Also, add `secure` for security. -->
