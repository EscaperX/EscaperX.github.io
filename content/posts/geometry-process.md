---
title: "Geometry Process in UE"
subtitle: ""
date: 2023-06-25T17:59:34+08:00
lastmod: 2023-06-25T17:59:34+08:00
draft: true
author: ""
authorLink: ""
description: ""
license: ""
images: []

tags: [GeometryProcess]
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

# DynamicMesh

DynamicMesh is actually a similiar data structure with half-edge representation which provides connectivity and orientation of mesh.

DynamicMesh stores vertices, per-vertex vertex normals, colors, uvs and a list of connected edges.

For edges, it stores two vertices and two adjacent triangles (if it is boundary, leave the latter one invalid). So In a "ordinary" (I know nothing about manifold so I could just use "oridnary" to represent a pretty mesh) mesh, so you can traverse all the edges in order following the adjacent triangles. (What if two opposite cones with the overlap peak?)


