---
title: 组件库DQ
subtitle:
date: 2023-10-21T20:04:12+08:00
draft: true
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
math: false
lightgallery: false
password:
message:
repost:
  enable: true
  url:

# See details front matter: https://fixit.lruihao.cn/documentation/content-management/introduction/#front-matter
---

<!--more-->

## TS

TS是静态编译工具，可以帮我们生成对应的JS代码。而项目开发中常常需要使用JS之外的库，which TS不知道它们是什么类型的，这时候需要加一个声明文件，格式是xxx.d.ts. （d是declare的意思）， 其目的是为了给实际的业务逻辑代码提供类型。声明中没有实际的实现代码，只有类型声明。比如，给axios加一个类型声明：

```typescript
declare function axios(url: string): string
或者
interface Axios {
    get: (url:string) => string;
    post: (url: string, data: any) => string
}

declare const axios: Axios
```

很多时候开发者都会写好声明文件，所以不用自己写了。需要的情况一般是，原来的模块是JS写的，现在想要在TS项目中再次使用之前JS写的模块。如果你的项目本身就是TS的，那么我们是不需要写这个定义文件的，因为我们的库在经过tsc编译以后，不仅会有JS代码，还会自动生成一个.d.ts文件。

注意axios是以库的形式存在，而不是一个全局变量。所以要`import axios from 'axios'`.



