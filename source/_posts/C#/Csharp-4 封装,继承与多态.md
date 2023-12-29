---
date: 2023-12-28 14:13
title: Csharp-4 封装,继承与多态
tags: 
cover: https://raw.githubusercontent.com/silentwaver/DrawBed/main/images/202312291916086.JPG
---
## 封装
封装的目的:防止对实现细节的访问,对外部访问做有效控制,维护数据的有效性,安全性

C#通过访问修饰符控制类成员的范围和可见性
C# 支持的访问修饰符如下所示：
- public：所有对象都可以访问；
- private：对象本身在对象内部可以访问,类的实例也无法访问该成员
- protected：只有该类对象及其子类对象可以访问
- internal：同一个程序集的对象可以访问；(同一程序集指namespace相同)
- protected internal：访问限于当前程序集或派生自包含类的类型。

生动形象(  
房子=namespace,B,D为A子类,A,B,C位于同一namespace下,D位于不同namespace下
![](../../assets/Pasted%20image%2020231228145422.png)


## 继承
继承允许根据一个类来定义另一个类,有利于代码的重用.已有的类称为基类,新的类称为派生类.派生类会继承基类所有可继承成员

**C# 不支持多重继承**。但是可以使用接口来实现多重继承。一个类可以派生自一个类或多个接口,用逗号分隔
```C#
<访问修饰符> class <基类>
{
 ...
}
class <派生类> : <基类>,<接口1>,<接口2> 
{
 ...
}
```


## 多态
多态是同一个行为具有多个不同表现形式或形态的能力。
**多态性**意味着有多重形式。在面向对象编程范式中，多态性往往表现为"一个接口，多个功能"。

多态就是同一个接口，使用不同的实例而执行不同操作.

多态可以是静态或动态的.静态多态性函数相应发生在编译时,动态多态性函数响应发生在运行时

在 C# 中，每个类型都是多态的，因为包括用户定义类型在内的所有类型都继承自 Object。

### 静态多态
#### 函数重载(overload)
在一个类里可以有多个函数名相同,参数不同(参数数量,参数类型),返回类型相同或不通过的方法

#### 运算符重载
您可以重定义或重载 C# 中内置的运算符。因此，程序员也可以使用用户自定义类型的运算符。重载运算符是具有特殊名称的函数，是通过关键字 **operator** 后跟运算符的符号来定义的。与其他函数一样，重载运算符有返回类型和参数列表。

<details>
<summary>实例</summary>
	 <pre><code>
	 using System;
	 namespace OperatorOvlApplication {
	 class Box {
	      private double length;      // 长度
	      private double breadth;     // 宽度
	      private double height;      // 高度
	      
	      public double getVolume()  {
	         return length * breadth * height;
	      }
	      public void setLength( double len )
	      {
	         length = len;
	      }
	
	      public void setBreadth( double bre )
	      {
	         breadth = bre;
	      }
	
	      public void setHeight( double hei )
	      {
	         height = hei;
	      }
	      // 重载 + 运算符来把两个 Box 对象相加
	      public static Box operator+ (Box b, Box c)
	      {
	         Box box = new Box();
	         box.length = b.length + c.length;
	         box.breadth = b.breadth + c.breadth;
	         box.height = b.height + c.height;
	         return box;
		      }
	
	   }
	
	   class Tester
	   {
	      static void Main(string[] args)
	      {
	         Box Box1 = new Box();         // 声明 Box1，类型为 Box
	         Box Box2 = new Box();         // 声明 Box2，类型为 Box
	         Box Box3 = new Box();         // 声明 Box3，类型为 Box
	         double volume = 0.0;          // 体积
	
	         // Box1 详述
	         Box1.setLength(6.0);
	         Box1.setBreadth(7.0);
	         Box1.setHeight(5.0);
	
	         // Box2 详述
	         Box2.setLength(12.0);
	         Box2.setBreadth(13.0);
	         Box2.setHeight(10.0);
	
	         // Box1 的体积
	         volume = Box1.getVolume();
	         Console.WriteLine("Box1 的体积： {0}", volume);
	
	         // Box2 的体积
	         volume = Box2.getVolume();
	         Console.WriteLine("Box2 的体积： {0}", volume);
	
	         // 把两个对象相加
	         Box3 = Box1 + Box2;
	
	         // Box3 的体积
	         volume = Box3.getVolume();
	         Console.WriteLine("Box3 的体积： {0}", volume);
	         Console.ReadKey();
	      }
	   }
	}
	 </code></pre>

</details>

### 动态多态

### 重写(override)

使用抽象类,抽象方法以及需方法进行重写

重写的方法需加上关键字**override**

#### 抽象类 抽象方法
C# 允许您使用关键字 **abstract** 创建抽象类与抽象方法，用于提供接口的部分类的实现。当一个派生类继承自该抽象类时，实现即完成。**抽象类**包含抽象方法，抽象方法可被派生类实现。派生类具有更专业的功能。

请注意，下面是有关抽象类的一些规则：

- 您不能创建一个抽象类的实例。
- 您不能在一个抽象类外部声明一个抽象方法。
- 通过在类定义前面放置关键字 **sealed**，可以将类声明为**密封类**。当一个类被声明为 **sealed** 时，它不能被继承。抽象类不能被声明为 sealed。

> 如果父类的方法本身不需要实现任何功能，仅仅是为了定义方法签名，目的是让子类去覆写它，那么，可以把父类的方法声明为抽象方法
> 
> 抽象方法只能存在于抽象类中
> 
> 抽象类可以强迫子类实现其定义的抽象方法，否则编译会报错。因此，抽象方法实际上相当于定义了“规范”。
> 
> 可以通过抽象类类型去引用具体的子类的实例,这样就可以忽略子类实际类型

#### 虚方法
当有一个定义在类中的函数需要在继承类中实现时，可以使用**虚方法**。虚方法是使用关键字 **virtual** 声明的。
虚方法可以在不同的继承类中有不同的实现。
对虚方法的调用是在运行时发生的。


> **抽象方法和虚方法的区别**
- 1.虚方法必须有实现部分，抽象方法没有提供实现部分，抽象方法是一种强制派生类覆盖的方法，否则派生类将不能被实例化。
- 2.抽象方法只能在抽象类中声明，虚方法不是。如果类包含抽象方法，那么该类也是抽象的，也必须声明类是抽象的。
- 3.抽象方法必须在派生类中重写，这一点和接口类似，虚方法不需要再派生类中重写。

简单说，抽象方法是需要子类去实现的。虚方法是已经实现了的，可以被子类覆盖，也可以不覆盖，取决于需求。抽象方法和虚方法都可以供派生类重写。
