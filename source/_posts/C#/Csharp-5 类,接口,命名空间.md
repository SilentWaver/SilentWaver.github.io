---
date: '2023-12-29 18:52'
title: 'Csharp-5 类,接口,命名空间'
categories:
  - C#
tags:
---

## 类(Class)
类默认是private的
### 构造函数
与类同名的一个成员函数,在创建类的新对象时执行.
构造函数无返回类型

### 析构函数
与类同名的函数,在函数名前加~作为前缀,会在对象生命周期结束时自动执行.通常用于释放资源
析构函数无返回值与参数,无法继承或重载

### 静态成员
我们可以使用 **static** 关键字把类成员定义为静态的。当我们声明一个类成员为静态时，意味着无论有多少个类的对象被创建，只会有一个该静态成员的副本。

关键字 **static** 意味着类中只有一个该成员的实例。
静态方法只能调用静态变量,无法直接调用非静态变量.

## 接口(Interface)
接口包含非抽象 [`class`](https://learn.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/class) 或 [`struct`](https://learn.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/struct) 必须实现的一组相关功能的定义
接口使用 **interface** 关键字声明，它与类的声明类似。接口声明默认是 public 的。
接口内不能有字段变量，构造函数. **接口内可以定义属性（有get和set的方法）**. 如string color { get ; set ; }这种。 实现接口时，必须和接口的格式一致。
如果一个接口继承其他接口，那么实现类或结构就需要实现所有接口的成员


## 命名空间(namespace)
**命名空间**的设计目的是提供一种让一组名称与其他名称分隔开的方式。在一个命名空间中声明的类的名称与另一个命名空间中声明的相同的类的名称不冲突。

为了调用支持命名空间版本的函数或变量，会把命名空间的名称置于前面：
```c#
namespace namespace_name
{
   // 代码声明
}
// 其他命名空间下
namespace_name.item_name;
```


### using关键字
**using** 关键字表明程序使用的是给定命名空间中的名称。例如，我们在程序中使用 **System** 命名空间，其中定义了类 Console。我们可以只写：
```c#
Console.WriteLine ("Hello there");
```

### 嵌套命名空间

命名空间可以被嵌套，即您可以在一个命名空间内定义另一个命名空间，使用点（.）运算符访问嵌套的命名空间的成员,如下所示：
```c#
namespace namespace_name1 
{
   // 代码声明
   namespace namespace_name2 
   {
     // 代码声明
   }

using namespace_name1;  
using namespace_name1.namespace_name2;
```