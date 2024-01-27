---
date: '2024-01-02 16:16'
title: 'Csharp-7 特性,反射,属性'
categories:
  - C#
tags:
---
## 属性(Property)
**属性（Property）** 是类（class）、结构（structure）和接口（interface）的命名（named）成员。类或结构中的成员变量或方法称为 **域（Field）**。属性（Property）是域（Field）的扩展，且可使用相同的语法来访问。它们使用 **访问器（accessors）** 让私有域的值可被读写或操作。

属性（Property）不会确定存储位置。相反，它们具有可读写或计算它们值的 **访问器（accessors）**。
例如，有一个名为 Student 的类，带有 age、name 和 code 的私有域。我们不能在类的范围以外直接访问这些域，但是我们可以拥有访问这些私有域的属性。

### 抽象属性（Abstract Properties）

抽象类可拥有抽象属性，这些属性应在派生类中被实现。

## 索引器(Indexer)
索引器用来为多个数据成员提供访问器(get,set),可以不通过点语法而直接通过索引访问对象的域

```C#
element-type this[int index] 
{
   // get 访问器
   get 
   {
      // 返回 index 指定的值
   }

   // set 访问器
   set 
   {
      // 设置 index 指定的值 
   }
}
```

索引器（Indexer）可被重载。索引器声明的时候也可带有多个参数，且每个参数可以是不同的类型。没有必要让索引器必须是整型的。C# 允许索引器可以是其他类型，例如，字符串类型。

## 特性(Attribute)



## 反射(Reflection)

