---
date: 2023-12-29 19:47
title: Csharp-6 其他一些基础概念
tags:
---
## 预处理器指令
预处理器指令指导编译器在实际编译开始之前对信息进行预处理。
所有的预处理器指令都是以 # 开始。且在一行上，只有空白字符可以出现在预处理器指令之前。预处理器指令不是语句，所以它们不以分号（;）结束。

|预处理器指令|描述|
|---|---|
|\#define |它用于定义一系列成为符号的字符。|
|\#undef |它用于取消定义符号。|
|\#if |它用于测试符号是否为真。条件为假的代码不会被编译 |
|\#else |它用于创建复合条件指令，与 \#if 一起使用。 |
|\#elif |它用于创建复合条件指令。|
|\#endif |指定一个条件指令的结束。|
|\#line |它可以让您修改编译器的行数以及（可选地）输出错误和警告的文件名。|
|\#error |它允许从代码的指定位置生成一个错误。|
|\#warning |它允许从代码的指定位置生成一级警告。|
|\#region |它可以让您在使用 Visual Studio Code Editor 的大纲特性时，指定一个可展开或折叠的代码块。|
|\#endregion |它标识着\#region 块的结束。 |
## 异常处理

- **try**：一个 try 块标识了一个将被激活的特定的异常的代码块。后跟一个或多个 catch 块。
- **catch**：程序通过异常处理程序捕获异常。catch 关键字表示异常的捕获。
- **finally**：finally 块用于执行给定的语句，不管异常是否被抛出都会执行。例如，如果您打开一个文件，不管是否出现异常文件都要被关闭。
- **throw**：当问题出现时，程序抛出一个异常。使用 throw 关键字来完成。
### C# 中的异常类

C# 异常是使用类来表示的。C# 中的异常类主要是直接或间接地派生于 **System.Exception** 类。**System.ApplicationException** 和 **System.SystemException** 类是派生于 System.Exception 类的异常类。

**System.ApplicationException** 类支持由应用程序生成的异常。所以程序员定义的异常都应派生自该类。

**System.SystemException** 类是所有预定义的系统异常的基类。

下表列出了一些派生自 System.SystemException 类的预定义的异常类：

|异常类|描述|
|---|---|
|System.IO.IOException|处理 I/O 错误。|
|System.IndexOutOfRangeException|处理当方法指向超出范围的数组索引时生成的错误。|
|System.ArrayTypeMismatchException|处理当数组类型不匹配时生成的错误。|
|System.NullReferenceException|处理当依从一个空对象时生成的错误。|
|System.DivideByZeroException|处理当除以零时生成的错误。|
|System.InvalidCastException|处理在类型转换期间生成的错误。|
|System.OutOfMemoryException|处理空闲内存不足生成的错误。|
|System.StackOverflowException|处理栈溢出生成的错误。|

### 创建用户自定义异常
您也可以定义自己的异常。用户自定义的异常类是派生自 **ApplicationException** 类。

## 文件输入输出
c#中文件按**流**处理

### C# I/O 类

System.IO 命名空间有各种不同的类，用于执行各种文件操作，如创建和删除文件、读取或写入文件，关闭文件等。

下表列出了一些 System.IO 命名空间中常用的非抽象类：

|I/O 类|描述|
|---|---|
|BinaryReader|从二进制流读取原始数据。|
|BinaryWriter|以二进制格式写入原始数据。|
|BufferedStream|字节流的临时存储。|
|Directory|有助于操作目录结构。|
|DirectoryInfo|用于对目录执行操作。|
|DriveInfo|提供驱动器的信息。|
|File|有助于处理文件。|
|FileInfo|用于对文件执行操作。|
|FileStream|用于文件中任何位置的读写。|
|MemoryStream|用于随机访问存储在内存中的数据流。|
|Path|对路径信息执行操作。|
|StreamReader|用于从字节流中读取字符。|
|StreamWriter|用于向一个流中写入字符。|
|StringReader|用于读取字符串缓冲区。|
|StringWriter|用于写入字符串缓冲区。|
## FileStream 类

System.IO 命名空间中的 **FileStream** 类有助于文件的读写与关闭。该类派生自抽象类 Stream。

您需要创建一个 **FileStream** 对象来创建一个新的文件，或打开一个已有的文件。创建 **FileStream** 对象的语法如下：

```c#
FileStream <object_name> = new FileStream( <file_name>,
<FileMode Enumerator>, <FileAccess Enumerator>, <FileShare Enumerator>);
```
例如，创建一个 FileStream 对象 **F** 来读取名为 **sample.txt** 的文件：
```c#
FileStream F = new FileStream("sample.txt", FileMode.Open, FileAccess.Read, FileShare.Read);
```

|参数|描述|
|---|---|
|FileMode|**FileMode** 枚举定义了各种打开文件的方法。FileMode 枚举的成员有：<br><br>- **Append**：打开一个已有的文件，并将光标放置在文件的末尾。如果文件不存在，则创建文件。<br>- **Create**：创建一个新的文件。如果文件已存在，则删除旧文件，然后创建新文件。<br>- **CreateNew**：指定操作系统应创建一个新的文件。如果文件已存在，则抛出异常。<br>- **Open**：打开一个已有的文件。如果文件不存在，则抛出异常。<br>- **OpenOrCreate**：指定操作系统应打开一个已有的文件。如果文件不存在，则用指定的名称创建一个新的文件打开。<br>- **Truncate**：打开一个已有的文件，文件一旦打开，就将被截断为零字节大小。然后我们可以向文件写入全新的数据，但是保留文件的初始创建日期。如果文件不存在，则抛出异常。|
|FileAccess|**FileAccess** 枚举的成员有：**Read**、**ReadWrite** 和 **Write**。|
|FileShare|**FileShare** 枚举的成员有：<br><br>- **Inheritable**：允许文件句柄可由子进程继承。Win32 不直接支持此功能。<br>- **None**：谢绝共享当前文件。文件关闭前，打开该文件的任何请求（由此进程或另一进程发出的请求）都将失败。<br>- **Read**：允许随后打开文件读取。如果未指定此标志，则文件关闭前，任何打开该文件以进行读取的请求（由此进程或另一进程发出的请求）都将失败。但是，即使指定了此标志，仍可能需要附加权限才能够访问该文件。<br>- **ReadWrite**：允许随后打开文件读取或写入。如果未指定此标志，则文件关闭前，任何打开该文件以进行读取或写入的请求（由此进程或另一进程发出）都将失败。但是，即使指定了此标志，仍可能需要附加权限才能够访问该文件。<br>- **Write**：允许随后打开文件写入。如果未指定此标志，则文件关闭前，任何打开该文件以进行写入的请求（由此进程或另一进过程发出的请求）都将失败。但是，即使指定了此标志，仍可能需要附加权限才能够访问该文件。<br>- **Delete**：允许随后删除文件。|
