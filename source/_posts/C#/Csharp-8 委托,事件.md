---
date: 2024-01-03 13:22
title: Csharp-8 委托,事件
tags:
---
## 委托(Delegate)
**委托（Delegate）** 是存有对某个方法的引用的一种引用类型变量。引用可在运行时被改变。
委托（Delegate）特别用于实现事件和回调方法。所有的委托（Delegate）都派生自 **System.Delegate** 类。
(感觉就是为了解决c#没有Function这个类型,因此用委托去声明一些类似的函数的一个类型,便于其他方法去调用时写类型)

```c#
delegate <return type> <delegate-name> <parameter list>
```

```c#

public delegate void GreetingDelegate(string name);

class Program
{
    private static void EnglishGreeting(string name)
    {
        Console.WriteLine("Good Morning, " + name);
    }
    private static void ChineseGreeting(string name)
    {
        Console.WriteLine("早上好, " + name);
    }
    private static void GreetPeople(string name, GreetingDelegate MakeGreeting)
    {
        MakeGreeting(name);
    }
    static void Main(string[] args)
    {
        GreetPeople("Liker", EnglishGreeting);
        GreetPeople("李志中", ChineseGreeting);
        Console.ReadLine();
    }
}
```

### 委托的多播（Multicasting of a Delegate）

委托对象可使用 "+" 运算符进行合并。一个合并委托调用它所合并的两个委托。只有相同类型的委托可被合并。"-" 运算符可用于从合并的委托中移除组件委托。

使用委托的这个有用的特点，您可以创建一个委托被调用时要调用的方法的调用列表。这被称为委托的 **多播（multicasting）**，也叫组播。

## 事件(Event)
C# 中使用事件机制实现线程间的通信。

事件在类中声明且生成，且通过使用同一个类或其他类中的委托与事件处理程序关联。包含事件的类用于发布事件。这被称为 **发布器（publisher）** 类。其他接受该事件的类被称为 **订阅器（subscriber）** 类。事件使用 **发布-订阅（publisher-subscriber）** 模型。

**发布器（publisher）** 是一个包含事件和委托定义的对象。事件和委托之间的联系也定义在这个对象中。发布器（publisher）类的对象调用这个事件，并通知其他的对象。

**订阅器（subscriber）** 是一个接受事件并提供事件处理程序的对象。在发布器（publisher）类中的委托调用订阅器（subscriber）类中的方法（事件处理程序）。

### 声明事件（Event）

在类的内部声明事件，首先必须声明该事件的委托类型。例如：
```c#
public delegate void BoilerLogHandler(string status);
```

然后，声明事件本身，使用 **event** 关键字：
```c#
// 基于上面的委托定义事件
public event BoilerLogHandler BoilerEventLog;
```

[委托与事件示例](https://www.cnblogs.com/SkySoot/archive/2012/04/05/2433639.html)
