---
layout: post
title: "JavaScript: Equality Operators and their evil twins. "
subtitle: "careful with that equality operator..."
date: 2013-01-09 23:30:00 -0600
published: true
permalink: /2013/01/09/js-equality-operator/
disclaimer: true
categories: ['Programming']
tags:
 - javascript
---

There are four operators supported by JavaScript that one can use to check conditions for equality.  == and != as with most of the high level languages. But they work differently.

```javascript
var five = 5;
if( five == '5')
   alert('The type is converted for you !'); // JavaScript executes this one !!!
else
   alert('integer and string are different'); // This statement is executed in most of the typed high level languages.
```

What happens here is JavaScript automatically converts the type and then does checking. So we need to be extra cautious while using these operators, as they can result in some undesired results.
If you need to consider type safe checking then JavaScript provide another set of operators === and !==. These work in more familiar way as any other high level programming language. With these operators the JS engine will return if both the type and value are same otherwise false.
Is there any other difference? One might quickly ask. Well, it cases when the checking is done on same type there won’t be any difference, but in cases where the == and != does type conversion some very little performance effect would be there and these operators will be slow to execute when compared to === and !==.

Also there can be some inconsistencies in the way == and != are executed, hence its advised to use === and !== in most cases.

To is also ascertained by well-known JavaScript guru Douglas Crockford's in his excellent book

[JavaScript: The Good Parts](http://www.amazon.com/gp/product/0596517742/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0596517742&linkCode=as2&tag=seshusviews-20&linkId=4KM4Y2YUBRM2QM6Q)

> JavaScript has two sets of equality operators: === and !==, and their evil twins == and !=. The good ones work the way you would expect. If the two operands are of the same type and have the same value, then === produces true and !== produces false. The evil twins do the right thing when the operands are of the same type, but if they are of different types, they attempt to coerce the values. the rules by which they do that are complicated and unmemorable. These are some of the interesting cases:

```javascript
'' == '0'           // false
0 == ''             // true
0 == '0'            // true

false == 'false'    // false
false == '0'        // true

false == undefined  // false
false == null       // false
null == undefined   // true

' \t\r\n ' == 0     // true
```
>The lack of transitivity is alarming. My advice is to never use the evil twins. Instead, always use ===and !==. All of the comparisons just shown produce false with the === operator.

##### *Watch out for these differences while implementing JavaScript.*
