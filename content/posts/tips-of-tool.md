---
title: "Tips of Tool"
subtitle: ""
date: 2023-07-23T22:48:50+08:00
lastmod: 2023-07-23T22:48:50+08:00
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
Here're some tips on the common build tools like git, cmake, shell and so on.
<!--more-->

# Git

# Shell

# Cmake

## Learn Cmake from Explosion

## Learn from OpenXLSX

[OpenXLSX](https://github.com/troldal/OpenXLSX) is a great library for Microsoft Excel files, which also provides an reduced but complete 
CMakeList file. 

```cmake
#=======================================================================================================================
# Preamble
#=======================================================================================================================
cmake_minimum_required(VERSION 3.15 FATAL_ERROR)
project(OpenXLSX VERSION 0.4.1 LANGUAGES CXX)

set(CMAKE_CXX_VISIBILITY_PRESET hidden)
set(CMAKE_VISIBILITY_INLINES_HIDDEN YES)

#=======================================================================================================================
# Set C/C++ compiler version
#=======================================================================================================================
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
set(IGNORE_ME ${CMAKE_C_COMPILER}) # Suppress CMake warning message

#=======================================================================================================================
# Output Directories.
#=======================================================================================================================
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/output)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/output)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/output)

#=======================================================================================================================
# Add build options
#=======================================================================================================================
option(OPENXLSX_CREATE_DOCS "Build library documentation (requires Doxygen and Graphviz/Dot to be installed)" ON)
option(OPENXLSX_BUILD_SAMPLES "Build sample programs" ON)
option(OPENXLSX_BUILD_TESTS "Build and run library tests" ON)
option(OPENXLSX_BUILD_BENCHMARKS "Build and run library benchmarks" ON)
option(OPENXLSX_ENABLE_LIBZIP "Enable using libzip" OFF)

#=======================================================================================================================
# Add project subdirectories
#=======================================================================================================================
add_subdirectory(OpenXLSX)

if(${OPENXLSX_CREATE_DOCS})
    add_subdirectory(Documentation)
endif()
```
### function

### 