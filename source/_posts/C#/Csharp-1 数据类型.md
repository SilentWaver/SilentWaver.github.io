---
title: Csharp-1 数据类型
categories:
  - C#
date: 2023-12-27 00:00:00
tags:
---
## 数据类型
### 值类型
包括bool,char以及大量数字类型,bool型默认值为false,char默认为‘\\0'
数字类型包括浮点类double,float,有符号整数类byte(8位),short(16位),int(32位),long(64位),无符号整数类sbyte,ushort,uint,ulong,以及128位精确十进制值decimal.double型默认值为0.0D,float为0.0F,decimal为0.0M,long为0.0L,其余类型为0

### 引用类型
#### Object(对象)
对象是C#通用类型系统(CTS)所有类型的终极基类,是System.Object的别名.
当一个值类型转换为对象类型时，则被称为 **装箱**；另一方面，当一个对象类型转换为值类型时，则被称为 **拆箱**

#### Dynamic(动态)
可以存储任何类型的值,类型检查在运行时发生
对象类型变量的类型检查是在编译时发生的，而动态类型变量的类型检查是在运行时发生的

#### String(字符串)
C# string 字符串的前面可以加 @（称作"逐字字符串"）将转义字符（\\）当作普通字符对待，比如：
```C#
string str = @"C:\Windows";
// 等价于
string str = "C:\\Windows";
```

@ 字符串中可以任意换行，换行符及缩进空格都计算在字符串长度之内。

```C#
string str = @"<script type=""text/javascript"">
    <!--
    -->
</script>";
```

### 指针类型(Pointer types)
用于存储另一类型的内存地址
声明指针类型的语法：
```C#
type* identifier;
//例如：
char* cptr;
int* iptr;
```

## 数据类型转换

### 隐式类型转换
从较小范围的类型转为较大类型范围时无需显式转换,编译器会自动转换.如从byte->int
### 显式类型转换
C#提供了较多的显示转换类型方法


