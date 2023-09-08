---
title: "Computer System: A Programmer's Perspective"
subtitle: ""
date: 2023-09-06T09:59:43+08:00
lastmod: ["lastmod", ":git", "date", "publishDate"]
draft: false
author: ""
authorLink: ""
description: ""
license: ""
images: []

tags: []
categories: []

featuredImage: ""
featuredImagePreview: ""

hiddenFromHomePage: false
hiddenFromSearch: false
twemoji: false
lightgallery: true
ruby: true
fraction: true
fontawesome: true
linkToMarkdown: true
rssFullText: false

toc:
  enable: true
  auto: true
code:
  copy: true
  maxShownLines: 50
math:
  enable: true
  # ...
mapbox:
  # ...
share:
  enable: true
  # ...
comment:
  enable: true
  # ...
library:
  css:
    # someCSS = "some.css"
    # located in "assets/"
    # Or
    # someCSS = "https://cdn.example.com/some.css"
  js:
    # someJS = "some.js"
    # located in "assets/"
    # Or
    # someJS = "https://cdn.example.com/some.js"
seo:
  images: []
  # ...
---

Useful topics in CSAPP

<!--more-->

**Prelude**: The notes provided here are not simply copied from the textbook. I select topics that suprise me, focusing on comparing the different explanations or
examing practical applications. So I would omit many conventional definitions and derivations. I wil be very happy if these notes assist you in comprehending various concepts or understanding the underlying reasons.

# Representing and Manipulating information

## Two's-Complement Encodings

The definition in the book is new to me:
> For vector $\overrightarrow{x} = {x_{w-1}, x_{w-2}, \dots, x_0}$:
> $$B2T_w(\overrightarrow{x}) = -x_{w-1}2_{w-1} + \sum_{i=0}^{w-2}x_i 2^i$$

It means that when the most significant bit is 1, the number is counted from $-2^{w-1}$

As usually observed in Chinese textbook, *reverse encoding* is introduced to illustrate the concept of two's complement encoding.
In *reverse encoding*, for a non-negetive number $x  = {0, x_{w-2}, \dots, x_0}$, the reverse encoding retains the same bits as $x$, but for negtive $x = {1, x_{w-2}, \dots, x_0}$, get reversed by bit except for the most significant bit representing for the sign.

Based on *reverse encoding*, the 2's complement encoding of non-negtive numbers preserves the same bits. However, for negative numbers, this encoding is obtained by adding 1 to *reverse encoding*.

This is not intuitive, but we can establish the connection between this complex procedure with the origin definition, obtain the 2-complement encodings of -x, where x is non-negtive number.

For a non-negative number $x$ with 2's complement encoding of ${0, x_{w-2}, \dots, x_0}$, suppose a negative number $y = x$ whose 2-complement encoding is ${1, y_{w-2}, \dots, y_0}$.
So we have:
$$-2^{w-1} + \sum_{i=0}^{w-2} y_i 2^i = -x$$

So the value of bits, except for the sign bit, is actually $2^{w-1} - x$. And the process of "reverse bit and add 1" euqals to "{1, 1, ..., 1} - x + 1". They are the same.

We can also find that the unsigned value of the 2's complement encoding is $2^w - x$. That's what "2's complement" represents.

### Shfiting

As it is widely known that it's dangerous to convert between signed and unsigned value.
And based on the 2's complement encoding, here're some behaviours:
```c++
void print(unsigned char *p, int len) {
    for (int i = 0; i < len; i++) {
        printf("%.2x,", *p);
        p+=1;
    }
}

int y = 2147483648;
// y = 0x80000000 = -1;
// print: 00, 00, 00, 80

y <<= 1;
// y = 0;

y = -1;
// 0xffffffff
y >>= 1;
// 0xffffffff still -1

y = 2147482647
// y = 0x7fffffff the largest number of int
y <<= 1;
// y = 0xfffffffe = -2
```

We can also find the operating system is little-endian.

## Integer Arithmetic

### Unsigned Addition

Unsigned Addition is actually modular addition, which forms an *abelian group*.
Although I know nothing about the theory of group, I would take it natural that the modular addtion has an identity element 0 and every element has an additive inverse,
just like what we see in natrual numbers and vectors in linear algebra.

The following discussion is based on the hypothesis that $x$ and $y$ are unsigned integers represented by $w$ bits.

- How to detect overflow?

We know that $x + y \geq x$ if there's no overflow. And at "most" time the result will be smaller than $x$ if an overflow occurs.
But is it possible that we may choose a $y$ that $x + y > 2^w > x$ ? No, unless $y > 2^w$ that will never happen.

So simply `return x + y < x;` is enough.

- What's the additive inverse of $x$?

This actually has been discussed in the previous section, "the unsigned value of the 2's complement encoding is $2^w - x$".
Because the 2's complement encoding of non-negtive value is the same to its binary representation ,and there's no concept of "nagative" here,
so everything is suitable here.

But this proof is still too complicated. A intuitive explanation is, in unsigned addition we have $2^w = 0$. $x + (-x) = 2^w$, so $(-x) = 2^w - x$.
