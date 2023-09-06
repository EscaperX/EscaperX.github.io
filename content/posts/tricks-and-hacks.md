---
title: "Tricks and Hacks"
subtitle: ""
date: 2023-09-06T11:45:07+08:00
lastmod: 2023-09-06T11:45:07+08:00
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
### std::string and c-style strings

`std::string` can hold `'\0'`, but if use c-style string to construct a std::string, it will iterate from the start pointer and stop at the first `\0`.
But you can also specify the length or using `std::string_literals;` to avoid that.
```c++
std::string str = "12345";
str[3] = '\0';
std::cout << str;
// output: 1235
std::string str("123\05");
std::cout << str;
// output: 123
std::string str("123\05", 5);
std::cout << str;
// output: 1235
```


