---
title: CSAPP 2.Representing and Manipulating Information
subtitle:
date: 2023-09-21T20:04:24+08:00
draft: false
author:
  name:
  link:
  email:
  avatar:
description:
keywords:
license:
comment: false
weight: 0
tags:
  - draft
categories:
  - draft
hiddenFromHomePage: false
hiddenFromSearch: false
summary:
resources:
  - name: featured-image
    src: featured-image.jpg
  - name: featured-image-preview
    src: featured-image-preview.jpg
toc: true
math: true
lightgallery: false
password:
message:
repost:
  enable: true
  url:

# See details front matter: https://fixit.lruihao.cn/documentation/content-management/introduction/#front-matter
---

<!--more-->

> In this chapter, we examine the fundamental properties of how numbers and other forms of data are represented on a computer and the properties of the operations that computers perform on these data.



## Reading

### Summary

Information Storage

Integer Representations

Integer Arithmetic（整数运算）

Floating Point

why binary?  The electronic circuitry for storing and performing computations on tow-valued signals is very simple and reliable.

#### C memory layout

At runtime, the loader tells your OS to give your program a big blob of memory.

On a 32-bit system. the memory has 32-bit addresses. Each bit can be a 0 or a 1, so you have $2^{32}$ addresses.

Each address refers to one byte, which means you have $2^{32}$ bytes of memory.

在计算机中存储器的容量是以**字节**为基本单位的，一个内存地址代表一个字节（8 bits）的存储空间。

```goat

+--------------------------------------------------------------------------------------------------+
|                                                                                                  |
+--------------------------------------------------------------------------------------------------+
^                                                                                                  ^
|                                                                                                  |
address 0x00000000                                                                              address 0xFFFFFFFF   

```

One long row of bytes is hard  to read, so we usually draw memory as a grid of bytes. 

This is only for clarity. The program still sees the long row of bytes on the above.

```goat
address 0xFFFFFFFF+---------------------+                          
                  |                     |                                                                        
                  |                     |                                                                               
                  |                     |
                  |                     |
                  |                     |
                  |                     |
                  |                     |
                  |                     |
                  |                     |
                  |                     |
                  |                     |
                  |                     |
                  |                     |
                  |                     |
address 0x00000000+---------------------+
```



## Lecture

And it all comes down to the fact that they use finite representations of things that are potentially infinite in their expanse.

### Computer Arithmetic

#### Does not generate random values 

Arithmetic operations have important mathematical properties

#### Cannot assume all "usual" mathematical properties

- Due to finiteness of representations
- Integer operations satisfy "ring" properties: commutativity, associativity, distributivity.
- Floating point operations satisfy "ordering" properties: monotonicity, values of signs.

#### Observation

- Need to understand which abstractions apply in which contexts
- Important issues for complier writers and serious application programmer.