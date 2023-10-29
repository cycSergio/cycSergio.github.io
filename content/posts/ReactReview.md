---
title: ReactReview
subtitle:
date: 2023-10-13T22:53:57+08:00
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

## Ⅰ JS Review

### 1 Variable Declaration

There are 3 ways to declare a variables in JS: `let`, `const`, and `var`.

The difference is that `var` is a outdated way (`var` has NO block scope, only function scope and global scope) and should be avoided in most cases.

### 2 Destructing assignment (解构赋值)

```javascript
let a, b;
let arr = ['john', 'hug']
[a, b] = arr; // 等号左边不是数组的意思，是解构赋值的语法.这也是解构赋值最常用的场景

//或者直接 声明和赋值一起写
const [a, b] = arr;

//再一个场景
function fn() {
    return ['john', 'hug', 'issac', 'ali'];
}

const [a, b, ...c] = fn(); // ...变量，会接受后边剩余的所有元素，返回一个数组

//对象的解构
const obj = {
    name: 'hug',
    age: 18,
    gender: 'male',
}

let a, b, c;
({name: a, age: b, gender: c} = obj); //对象的解构看起来就没有数组解构那么简洁，所以使用起来也不如数组解构那么常见
//或者声明和赋值也写在一起
const {name:name, gender:gender, age:age} = obj; //如果变量名和属性名一致，可以只写一个
const {name, gender, age} = obj;

//利用数组解构来交换两个变量的位置，不需要利用中间变量
a = 10; 
b = 20;
[a, b] = [b, a]; 左边在解构，右边在创建一个数组。
```



## Ⅱ

## Ⅲ

------

# React Docs

组件里可以渲染其他组件，但是不要嵌套它们的定义（这样的代码非常慢，并且会产生bug），应该在顶层定义每个组件。当子组件需要使用父组件的数据时（更确切地说，是需要在父组件里面个性化地配置子组件的时候/给子组件传递参数的时候），需要通过`props`的形式进行传递，而不是嵌套定义哈。一个组件的行为、显示形态都可以用 `props` 来控制，就可以达到很好的可配置性。

props指向的是一个对象，它包含了父组件中传递的所有参数



React组件特别适合单元测试哦。通用测试框架Jest出场了捏！测试的精髓是assert，assert的使用需要框架来提供一些api哈（断言库）。

除了通用测试框架之外，还需要有能将我们的react组件渲染/挂载到我们的测试用例上的特殊工具捏！听说Airbnb发布的Enzyme这一款测试工具非常好哦，它的主要特点是链式语法。或者用官方的react testing library。





