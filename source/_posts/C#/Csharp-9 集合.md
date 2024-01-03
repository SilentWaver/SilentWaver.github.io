---
date: 2024-01-03 16:02
title: Csharp-9 集合
tags:
---

## C# 集合（Collection）

集合（Collection）类是专门用于数据存储和检索的类。这些类提供了对栈（stack）、队列（queue）、列表（list）和哈希表（hash table）的支持。大多数集合类实现了相同的接口。

集合（Collection）类服务于不同的目的，如为元素动态分配内存，基于索引访问列表项等等。这些类创建 Object 类的对象的集合。在 C# 中，Object 类是所有数据类型的基类。

### 各种集合类和它们的用法

下面是各种常用的 **System.Collection** 命名空间的类。点击下面的链接查看细节。

| 类 | 描述和用法 |
| ---- | ---- |
| [动态数组（ArrayList）](https://www.runoob.com/csharp/csharp-arraylist.html "C# ArrayList") | 它代表了可被单独**索引**的对象的有序集合。<br><br>它基本上可以替代一个数组。但是，与数组不同的是，您可以使用**索引**在指定的位置添加和移除项目，动态数组会自动重新调整它的大小。它也允许在列表中进行动态内存分配、增加、搜索、排序各项。 |
| [哈希表（Hashtable）](https://www.runoob.com/csharp/csharp-hashtable.html "C# Hashtable") | 它使用**键**来访问集合中的元素。<br><br>当您使用键访问元素时，则使用哈希表，而且您可以识别一个有用的键值。哈希表中的每一项都有一个**键/值**对。键用于访问集合中的项目。 |
| [排序列表（SortedList）](https://www.runoob.com/csharp/csharp-sortedlist.html "C# SortedList") | 它可以使用**键**和**索引**来访问列表中的项。<br><br>排序列表是数组和哈希表的组合。它包含一个可使用键或索引访问各项的列表。如果您使用索引访问各项，则它是一个动态数组（ArrayList），如果您使用键访问各项，则它是一个哈希表（Hashtable）。集合中的各项总是按键值排序。 |
| [堆栈（Stack）](https://www.runoob.com/csharp/csharp-stack.html "C# Stack") | 它代表了一个**后进先出**的对象集合。<br><br>当您需要对各项进行后进先出的访问时，则使用堆栈。当您在列表中添加一项，称为**推入**元素，当您从列表中移除一项时，称为**弹出**元素。 |
| [队列（Queue）](https://www.runoob.com/csharp/csharp-queue.html "C# Queue") | 它代表了一个**先进先出**的对象集合。<br><br>当您需要对各项进行先进先出的访问时，则使用队列。当您在列表中添加一项，称为**入队**，当您从列表中移除一项时，称为**出队**。 |
| [点阵列（BitArray）](https://www.runoob.com/csharp/csharp-bitarray.html "C# BitArray") | 它代表了一个使用值 1 和 0 来表示的**二进制**数组。<br><br>当您需要存储位，但是事先不知道位数时，则使用点阵列。您可以使用**整型索引**从点阵列集合中访问各项，索引从零开始。 |
| [列表(List)](https://learn.microsoft.com/zh-cn/dotnet/api/system.collections.generic.list-1) | 可泛型的数组,**List** 是个强类型，很安全。其次看那个尖括号，它是 C#2.0 时加入的泛型，所以并不存在像 **ArrayList**那样要拆/装箱以此造成性能浪费。 |
| [字典(Dictionary)](https://learn.microsoft.com/zh-cn/dotnet/api/system.collections.generic.dictionary-2?view=net-8.0) | 带泛型的键值对集合 |

[数组,ArrayList,List区别](https://blog.csdn.net/zhang_xinxiu/article/details/8657431)
简单来说,数组允许多维,初始化时需确定大小,数组元素类型固定.
ArrayList与List只允许存在一维,但可以构建列表的列表实现多维
ArrayList与List提供了一些方法,使得数组的操作更加容易.ArrayList不具有泛型,List具有泛型.对ArrayList的值类型元素进行操作会进行装拆箱,造成性能问题.
