---
title: "C++ and Computer Graphics Weekly-01"
subtitle: ""
date: 2023-10-19T22:14:31+08:00
lastmod: 2023-10-19T22:14:31+08:00
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

This series is inspired by [Graphics Programming weekly](https://www.jendrikillner.com/post) updated by Jendrik Lllner, which collected awesome articles on graphics programming posted last week.

I think it's a good way to record progress and get satisfaction, comparing to create a column and carefully write a survey for each topic. Of course sometimes it's still necessary to do that to discuss some topic deeply. But I'd like to write down every great article, video or anything fantasy I saw in fragmented time. 

Here's the first one.

<!--more-->

## C++

### [CRTP Series from Fluent C++](https://www.fluentcpp.com/2017/05/12/curiously-recurring-template-pattern/)

Although I still did not find a good place to use it, I know now that the service interface is implemented using this pattern to provide mandatory function `current()` in the core.

It seems that everybody hates virtual functions a lot, lol.

### [Inline Variable in C++17](https://zh-blog.logan.tw/2020/03/22/cxx-17-inline-variable/)

The example is intuitive and complete. Although it's difficult to discuss all the cases, as cpp is such a complicated language, this is a great introduction for inline mechanism in modern C++.

### [Performance Comparation between `std::variant` and Other Stuffs](https://stackoverflow.com/questions/57726401/stdvariant-vs-inheritance-vs-other-ways-performance)

This happened to me that there're quite a lot of events corresponding to different callbacks. It's very confusing which way is the best, simply switch, enum index for array or wrapping callback information by variant. I saw detailed discussion and progressive refinement on the implementation of benchmark.

## Graphics

### [Introduction to Color](https://jamie-wong.com/post/color/)

A great blog introduces color from a bulb to pixels on the monitor. It answered my question about what's the relationship between radiometry and photometry and how the intensity of light in photometry is evaluated. And the way is fantastic that it introduces color space from the slice of a rainbow cube to the color gamuts. I think I understand the sentence "There're some colors that you can never see from screen".