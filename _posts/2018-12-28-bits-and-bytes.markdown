---
layout: post
title:  "Bits and Bytes"
date:   2018-12-28 23:10:00 +0800
categories: 
---

**Bit** and **Byte** sound a little *bit* familiar but strange. Actually, I bet you hear a lot of it almost every day, and you see it literally every day, yet you never realize it carries some significance. You must have heard about the storage of a mobile phone or a computer in terms of **128 GBs**, where **GB** here is an acronym of **GigaBytes**. Thus, it might be easy for you to relate **KB**, **MB**, and even **TB** to the term of **Bytes**. The goal of this post is to illustrate the terms of *bits* and *bytes*, making it more accessible to everyone, and perhaps somehow useful in someone's future life or career.

### Bit

A bit refers nothing but a single unit in a *binary* system, that is, 1 and 0, the number you usually see in a hacker movie.

Thus, a bit can have two and only two possible values: 0 and 1.

It is a huge topic on why bits are used in computers. It would be not covered here, and I might write about it sometime in the unforeseeable future.

So far so good.

### x-bit System

**1-bit**
So far we have only one bit, and thus there are only two possibilities:
```
0 1
```
That is, 2 values.

**2-bit**
When there are two bits, the possibilities of all values would be:

```
00 01 10 11
```
In total that is 4 values.

**3-bit**
In a 3-bit system, each value would has 3 bits, and all the combinations would be 
```
000 
001 010 100
011 101 110
111
```
8 combinations.

The patterns is: a x-bit system would have 2^x( that is, 2 to the power of x) values.
A simple illustration table would be like
```
System			All Possible Combinations
1-bit			2^1 = 2
2-bit			2^2 = 4
3-bit			2^3 = 8
4-bit			2^4 = 16
5-bit			2^5 = 32
...
x-bit			2^x
```

### Byte

A byte is, commonly, 8-bit. Thus, a byte can have 2^8, that is, 256 combinations.

The *byte* family has some members, some common examples would be
```
KB			KiloByte		1024 bytes
MB			MegaByte		1024 KB
GB			GigaByte		1024 MB
TB			TeraByte		1024 GB
```
The above table applies to the processor or virtual storage, which programmers use a lot.
For disk storage, it might be a little bit different, you can refer [this article](https://pradeepedwin.wordpress.com/mb-gb-tb-pb-eb-zb-yb-bb/) for more information.

### Numbers

Let's take integer for an example.

Usually on a 64-bit machine, like the one I am using right now, an `integer` or `int` is usually **4 bytes**. Based on what we have learned from above, it could be deduced that 4 bytes would be equivalent to 32 bits, and a **32-bit** system would have 2^32 combinations of values, which is **4,294,967,296**.

Since integers could be positive or negative, as well as 0, all 4,294,967,296 combinations must be split in halves, of which one is for positive numbers, one is for negative numbers. Thus in most programming languages, the range for `integer` is from -2,147,483,648 to 2,147,483,647. The number of integers within this range would be exactly **4,294,967,296**.

### Characters

It is important to remmeber that a machine is not able to store a *character*, which in some senses is a graphical representation of human writing. All characters, of all languages, must be **encoded** before being saved to the machine. Usually the encoding would be a number. In English, the encoding is pretty simple, since there are only 26 letters. To encoding all the letters, both upper case and lower case, we need in total 52 numbers.

Of course we need some puntuations, so the commonly used ASCII table contains both all the English letters and the mostly used punctuations. The number of characters in the ASCII table is 256, because a character, in most programming languages, would be 1 byte only, that is, 8 bits, which has 256 combinations of values.

### Afterword

To really understand what a bit means to a machine and how it actually works to make things simple for human beings to manipulate the machine is such a huge topic that it might not be possible to be covered in this short post. However, just by understanding some basics of bit-and-byte, programming would be less confusing and much more accessible.

References:

[Bits and Bytes](https://web.stanford.edu/class/cs101/bits-bytes.html)

[MB, GB, TB, PB, EB, ZB, YB, BB](https://pradeepedwin.wordpress.com/mb-gb-tb-pb-eb-zb-yb-bb/)