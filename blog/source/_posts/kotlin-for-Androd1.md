---
title: kotlin for Androd (1)
date: 2017-06-11 20:25:51
tags: kotlin
categories: Android
---

## 概述

#### Android 中使用Kotlin
Kotlin是一个非常适合开发Android应用程序，拥有现代编程语言中的优势，在Android平台中使用没有任何限制。

* 兼容性  
  Kotlin完全兼容JDK6的版本，确保Kotlin的工程能够跑在任何老的Android平台上。在Andorid Studio和其它一些开发工具中能够完全兼容Kotilin工具。
* 性能  
  由于类似于二进制的数据结构，Kotlin程序和Java程序跑得是一样快的。由于Kotlin支持内联函数，使用lambdas写代码经常能够相同的java代码更快。
* 互操作性  
  Kotlin可以完全和Java兼容一起使用，允许在Kotlin工程中使用现有任何Java库。数据绑定和Dragger也都能使用。
* 足迹  
Kotin拥有一个非常紧凑的运行时库，能够进一步降低和减少使用中混淆。在真实的工程中，Kotlin只产生几百个方法和少于100k的文件大小在apk中。
* 编译时间  
Kotlin支持高效的增量编译，所以当有一些额外的过重的clean build的时候，增量的构建Kotlin通常要比java来的快
* 学习曲线  
对于一个java开发者来说，学习kotin是非常容易的。kotlin插件自动帮助我们把java代码转到Kotlin代码.[Kontlin Koans](http://kotlinlang.org/docs/tutorials/koans.html) 提供一系列kotlin的关键点和一些交互练习。

#### Android中使用Kotlin中的一些例子

Kotlin已经被很多大公司采用，他们分享了一些经验。  
Pinterest成功的在他们的项目中引入了Kotlin,每月使用人数在150w  
Basecamp是完全的Kotlin项目，他们说很多使用kotlin的开发者能够带来极大的快乐感和提高速度  
Keepsafe's App Lock也已经完全使用Kotlin,减少了30%的代码行开销和10%的代码方法开销。

#### Android开发中使用的工具
Kotlin开发团队提供了一系列Android 开发工具。  
[Kotlin Android Extensions](http://kotlinlang.org/docs/tutorials/android-plugin.html)是一个编译工具能够减少findViewById方法的调用。通过使用它提供的一些语义化的标签属性。  
[Anko](https://github.com/kotlin/anko)是一个库友善的封装了Android API的库，就像一种描述语言让你使用Kotlin代码代替使用layout.xml文件。

#### Next Step
* 下载[AS3.0](https://developer.android.com/studio/preview/index.html), 提供完全的Kotlin支持
* 跟着[Getting Started](http://kotlinlang.org/docs/tutorials/kotlin-android.html)创建你的Kotlin项目
* 想要更深入的学习，多看看[reference](http://kotlinlang.org/docs/reference/index.html)和[kotlin Koans](http://kotlinlang.org/docs/tutorials/koans.html)的文档
* 另一个资源所在地[Kotlin For Android](https://leanpub.com/kotlin-for-android-developers) 一本手把手教你创建Kotlin项目的图书。
* 学习google使用Kotlin编写的[项目](https://developer.android.com/samples/index.html?language=kotlin)。