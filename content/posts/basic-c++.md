---
title: "Basic C++"
subtitle: ""
date: 2023-08-11T13:10:29+08:00
lastmod: 2023-08-11T13:10:29+08:00
draft: true
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
  enable: false
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

<!--more-->
#### Built-in type: Array

<!--block-->
```c++
int a[10];
```
Is array `a` a pointer?
No. A pointer is a pointer, an array is an array.

When the array variable is used as value, it is usually implicitly converted to a pointer, which points to the first element in that array.
But when use as variable, it represents the whole array. For example, `sizeof a` gets the sizeof the whole array.

```c++
int *a = new int[10];
```
Is `a` an array or `*a` an array?

No. And you can never get the size of the malloced array when you loss the size at runtime.

What if missing the brackets when delete a malloced array?
Only the first element will be deleted.

What if delete a pointer which is casted?
In most cases it's undefined behaviour. [Here](https://stackoverflow.com/questions/2140319/can-i-new-then-cast-the-pointer-then-delete-safely-with-built-in-types-in) is a good discussion.

<!--[array, pointer]>
#### Operator

<!--block-->
`sizeof` is an unary operator, so all the behaviours follow the definition.

As consequnces: (It's important that you can't duduce backward from these behaviours to claim that sizeof is not a function)

- The operand of sizeof can be a parenthesised type, sizeof (int), instead of an object expression.
- The parentheses are unnecessary: int a; printf("%d\n", sizeof a); is perfectly fine. They're often seen, firstly because they're needed as part of a type cast expression, and secondly because sizeof has very high precedence, so sizeof a + b isn't the same as sizeof (a+b). But they aren't part of the invocation of sizeof, they're part of the operand.
- You can't take the address of sizeof.
- The expression which is the operand of sizeof is not evaluated at runtime (sizeof a++ does not modify a).
- The expression which is the operand of sizeof can have any type except void, or function types. Indeed, that's kind of the point of sizeof.

<!--[operator, sizeof]>

#### Forward declaration
<!--block-->
When to use forward declaration?

In Google's [style guide](https://google.github.io/styleguide/cppguide.html#Forward_Declarations), *Avoid using forward declarations where possible*

But when the circular reference is unavoidable, we can use forward declaration.

A great discussion about forward declaration: https://stackoverflow.com/a/553869

There's a case that the compiler will be misleading by forward declaration instead of just include header file:
```c++
// io.h
struct B {};
struct D: B{};
//test.h
void test(D* d);
// test.cc
struct B;
struct D;
void f(B* ) {
    std::cout << "f(B*)";
}
void f(void *) {
    std::cout << "f(void *)";
}
void test(D* d){
    f(d);
}
// main
#include "io.h"
#include "test.h"
int main() {
    D* d = new D();
    test(d);
}
```
The `f(void *)` is called, which is beyond expectation. This example also shows the working style of compiler.

<!--[project structure, forward declaration]-->

<!--block-->
#### Const and Function Overload
```c++
void f(const int);
void f(int);
```
It's not a valid function overload but a redefinition.
```c++
void f(const int &);
void f(int&);
int a;
f(a);
```
This is a valid function overload. Compiler will find a best suitable function for a variable a. If the parameter is simply a int, it will call `f(int &);`.
Because there's a implicit cast from int to const int, which may introduce overhead.
<!--[const, function overload]-->

## Undefined Behaviour

<!--block-->
What if a vector clears itself while a iterator is enumerating it?
<!--[iterator, vector]-->


# Idioms

## Pointer to implementation (PIMPL)
I'm quite curious that why cppref puts pimpl in *idiom* section. I use to regard it as a kind of design pattern.

<!--block-->

<!--[idiom, pimpl, design pattern]>
