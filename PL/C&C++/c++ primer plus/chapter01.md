# 第一章 预备知识
## 简介
C++融合了三种不同的编程方式：C语言代表的过程性语言、C++在C语言基础上添加的类代表的面向对象语言、C++模板支持的泛型编程。

汇编语言是低级（low-level）语言，即直接操作硬件，如直接访问CPU寄存器和内存单元。高级（high-level）语言致力于解决问题，而不针对特定的硬件。一种被称为编译器的特殊程序将高级语言翻译成特定计算机的内部语言。

一般来说，计算机语言要处理两个概念——**数据和算法**。C语言与当前最主流的语言一样，在最初面世时也是**过程性**（procedural）语言，这意味着它强调的是编程的算法方面。结构化编程将分支（决定接下来应执行哪个指令）限制为一小组行为良好的结构。另一个新原则是**自顶向下**（top-down）的设计。

与强调算法的过程性编程不同的是，OOP强调的是数据。在C++中，**类**是一种规范，它描述了这种新型数据格式，**对象**是根据这种规范构造的特定数据结构。类规定了可使用哪些数据来表示对象以及可以对这些数据执行哪些操作。OOP程序设计方法首先设计类,类定义描述了对每个类可执行的操作，然后您便可以设计一个使用这些类的对象的程序。从低级组织（如类）到高级组织（如程序）的处理过程叫做**自下向上**（bottom-up）的编程。

OOP还有助于创建可重用的代码，这将减少大量的工作。**信息隐藏**可以保护数据，使其免遭不适当的访问。**多态**让您能够为运算符和函数创建多个定义，通过编程上下文来确定使用哪个定义。**继承**让您能够使用旧类派生出新类。

**泛型编程（generic programming）**提供了执行常见任务（如对数据排序或合并链表）的工具。

**库**是编程模块的集合，可以从程序中调用它们。

## 程序创建
1. 使用文本编辑器编写程序，并将其保存到文件中，这个文件就是程序的**源代码**。
2. 编译源代码。这意味着运行一个程序，将源代码翻译为主机使用的内部语言——机器语言。包含了翻译后的程序的文件就是程序的**目标代码**（object code）。
3. 将目标代码与其他代码**链接**起来。例如，C++程序通常使用库。C++库包含一系列计算机例程（被称为函数）的目标代码。链接指的是将目标代码同使用的函数的目标代码以及一些标准的启动代码（startupcode）组合起来，生成程序的运行阶段版本。包含该最终产品的文件被称为**可执行代码**。

## 编译与链接