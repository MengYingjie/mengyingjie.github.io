---
title: 🤔为什么JAVA内部类要设计成静态和非静态
tags: 
- java
date: 2021-03-07 09:50:40
categories:
- java
- 技巧
---

> [⭐ 孟应杰的网站: myj.im ⭐](https://myj.im/)

### 📋两种内部类用法

```java
static class Outer {
	class Inner {}
	static class StaticInner {}
}

Outer outer = new Outer();
Outer.Inner inner = outer.new Inner();
Outer.StaticInner inner0 = new Outer.StaticInner();
```

### 🤔为什么设计内部类

1 在一个类内部，需要操作某种属性，而这个属性需要涉及的面又很广，我们可以考虑，将这些属性设计为内部类。

2 好比你设计类 B 的目的只是为了给类 A 使用，那么，我们就可将其设定为内部类，没有必要将类 B 设置成单独的 Java 文件，防止与其他类产生依赖关系。

### 🎲解释

根据Oracle官方的说法：
Nested classes are divided into two categories: static and non-static. Nested classes that are declared static are called ***static nested classes***. Non-static nested classes are called ***inner classes***.
从字面上看，一个被称为静态嵌套类，一个被称为内部类。

从字面的角度解释是这样的：

1 什么是嵌套？嵌套就是我跟你没关系，自己可以完全独立存在，但是我就想借你的壳用一下，来隐藏一下我自己（真TM猥琐）。没有你，我也可以创建实例.

2 什么是内部？内部就是我是你的一部分，我了解你，我知道你的全部（自由使用外部类的所有变量和方法），没有你就没有我。（所以内部类对象是以外部类对象存在为前提的）

### 🎬运用场景

1 那么，在设计内部类的时候我们就可以做出权衡：如果我内部类与你外部类关系不紧密，耦合程度不高，不需要访问外部类的所有属性或方法，那么我就设计成静态内部类。它可以降低包的深度，方便类的使用和管理类结构，而且，由于静态内部类与外部类并不会保存相互之间的引用，因此在一定程度上，还会节省那么一点内存资源，何乐而不为呢~~

2 既然上面已经说了什么时候应该用静态内部类，那么如果你的需求不符合静态内部类所提供的一切好处，你就应该考虑使用内部类了。最大的特点就是：你在内部类中需要访问有关外部类的所有属性及方法，我知晓你的一切... ... 

> 官网场景用例介绍
> 传送门：[http://docs.oracle.com/javase/](http://docs.oracle.com/javase/tutorial/java/javaOO/nested.html)

> 参考
> 链接：https://www.zhihu.com/question/28197253/answer/39814613


> 遇到此类问题，但看了文章还是未解决
> 评论或加 QQ：781378815