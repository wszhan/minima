---
layout: post
title:  "How to Convert List<A> to List<B>"
date:   2018-12-09 10:00:00 +0800
categories: 
---

I got this problem when I retrived a `List` of `Object`s from Spring RedisTemplate and treated them as my pojo objects like a `List` of `Student`.

The solution is easy as shown in the StackOverFlow answer:
```
List<TestB> variable = (List<TestB>)(List<?>) collectionOfListA;
```
This solution is to some extent controversial, because some think it is hacky for it is dodging the type safety Java provides, but some others consider it valid as long as we know what we are doing here.

Intuitively, `List<A>` is no different from `List<B>` except they have different parameters, but the outer type `List` is the same, both from the package `java.util`.
However, the reason underlying is that arrays in Java are covariant, but generics, in this case particularly, generic types of different parameters, or "concrete parameterized types", are not covariant. This has pros and cons, but they are out of the scope of this post.

References:

[How do you cast a List of supertypes to a List of subtypes?](https://stackoverflow.com/questions/933447/how-do-you-cast-a-list-of-supertypes-to-a-list-of-subtypes)