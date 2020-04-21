### C#知识点整理【一】

#### C#简介

- C# 是一个现代的、通用的、面向对象的编程语言，它是由微软（Microsoft）开发的，由 Ecma 和 ISO 核准认可的
- C# 是由 Anders Hejlsberg 和他的团队在 .Net 框架开发期间开发的
- C# 是专为公共语言基础结构（CLI）设计的。CLI 由可执行代码和运行时环境组成，允许在不同的计算机平台和体系结构上使用各种高级语言。
- C#成为一种广泛应用语言的优势： 
  - 现代的、通用的编程语言。
  - 面向对象。
  - 面向组件。
  - 容易学习。
  - 结构化语言。
  - 它产生高效率的程序。
  - 它可以在多种计算机平台上编译。
  - .Net 框架的一部分
- C#强大的编程功能
   虽然 C# 的构想十分接近于传统高级语言 C 和 C++，是一门面向对象的编程语言，但是它与 Java 非常相似，有许多强大的编程功能。

- C#的一些功能： 
  - 布尔条件（Boolean Conditions）
  - 自动垃圾回收（Automatic Garbage Collection）
  - 标准库（Standard Library）
  - 组件版本（Assembly Versioning）
  - 属性（Properties）和事件（Events）
  - 委托（Delegates）和事件管理（Events Management）
  - 易于使用的泛型（Generics）
  - 索引器（Indexers）
  - 条件编译（Conditional Compilation）
  - 简单的多线程（Multithreading）
  - LINQ 和 Lambda 表达式
  - 集成 Windows

#### .Net框架（.Net Framework）

- .Net 框架是一个创新的平台，能帮您编写出下面类型的应用程序 
  - Windows 应用程序
  - Web 应用程序
  - Web 服务
- .Net 框架应用程序是多平台的应用程序。框架的设计方式使它适用于下列各种语言：C#、C++、Visual Basic、Jscript、COBOL 等等。所有这些语言可以访问框架，彼此之间也可以互相交互
- .Net 框架由一个巨大的代码库组成，用于 C# 等客户端语言。下面列出一些 .Net 框架的组件 
  - 公共语言运行库（Common Language Runtime - CLR）
  - .Net 框架类库（.Net Framework Class Library）
  - 公共语言规范（Common Language Specification）
  - 通用类型系统（Common Type System）
  - 元数据（Metadata）和组件（Assemblies）
  - Windows 窗体（Windows Forms）
  - ASP.Net 和 ASP.Net AJAX
  - ADO.Net
  - Windows 工作流基础（Windows Workflow Foundation - WF）
  - Windows 显示基础（Windows Presentation Foundation）
  - Windows 通信基础（Windows Communication Foundation - WCF）
  - LINQ

[以上的内容摘自菜鸟](https://www.runoob.com/csharp/csharp-environment-setup.html)

#### CS文件结构

```
using System;
using System.Collections.Generic;
using System.Windows.Forms;    //引用命名空间，using 引用命名空间的关键字
【命名空间引用方式：using 命名空间 (命名空间可以使自己写的)】

namespace test_2020  //项目的命名空间，大多数也是项目本身的名称
{
    static class Program  //类名称，class 声明类的关键字
    {
        /// <summary>
        /// 应用程序的主入口点。
        /// </summary>
        [STAThread]
        static void Main()  //函数或者方法，Main 是程序起始点
        {
          ///用于写具体的方法函  
         Console.WriteLine("Hello World"); 
        }
    }
}

```

#### C#基本语法

注意：

- C#是大小写敏感的
- C#所有表达式必须以 ; 结尾
- C#与java不同，文件名可以不同于类名
- C#是一种面向对象的编程语言，在面向对象的程序设计方法中，程序由各种对象组成。相同种类的对象通常具有相同的类型。

关键字： 【对编译器有特殊意义的预订保留标识符，不能再做程序中的标识符】

- using ：引用命名空间
- namespace ： 声明命名空间
- class ： 声明类

注释：

```
 //  行注释
 /*注释内容*/  块注释
 /// 文档注释【可以用来解释类和方法】
        /// <summary>
        /// 描述这个方法的作用
        /// </summary>

```

变量:
 C#中每一个变量都有一个特定的数据类型，不同数据类型内存大小也不尽相同。

```
整数类型：byte（0-255），short（-32768-32767），int（-2*10^9-2*10^9【-2147483648-2147483647】），long（-9*10^18-9*10^18）

浮点型：float（-3.4*10^38-3.4*10^38）,double双精度类型（-5*10^~+-1.7*10^308）
float x = 1.1F;不加后缀F，系统会默认double类型
double y = 1.1;
double 可以包含：byte，short，int，long，float
十进制类型：decimal（-+7.9*10^28）  ：decimal z = 1.1M 不是基础类型，不能和float，double相互转换
布尔型：bool
字符串类型：string【string x = "Hello world" 切记加双引号  】 ，char【char x = "H"  只能一个】
string x = "Hello"+"world"
x.ToString() 转换成字符串方法
空类型：null 【本身就是一个值，不用申明】
string h = ""   放进去的内容为空
string H = null   空的什么都没放
数字类型和bool类型本身不可为null


```

#### C#数据类型

C#中变量类型



| 类型    | 描述                                      | 范围                                                    | 默认值 |
| ------- | ----------------------------------------- | ------------------------------------------------------- | ------ |
| bool    | 布尔值                                    | True 或 False                                           | False  |
| byte    | 8 位无符号整数                            | 0 到 255                                                | 0      |
| char    | 16 位 Unicode 字符                        | U +0000 到 U +ffff                                      | ‘\0’   |
| decimal | 128 位精确的十进制值，28-29 有效位数      | (-7.9 x 1028 到 7.9 x 1028) / 10^0 到 28^               | 0.0M   |
| double  | 64 位双精度浮点型                         | (+/-)5.0 x 10-324 到 (+/-)1.7 x 10308                   | 0.0D   |
| float   | 32 位单精度浮点型                         | -3.4 x 1038 到 + 3.4 x 1038                             | 0.0F   |
| int     | 32 位有符号整数类型                       | -2,147,483,648 到 2,147,483,647                         | 0      |
| long    | 64 位有符号整数类型                       | -9,223,372,036,854,775,808 到 9,223,372,036,854,775,807 | 0L     |
| sbyte   | 8 位有符号整数类型                        | -128 到 127                                             | 0      |
| short   | 16 位有符号整数类型	-32,768 到 32,767  | 0                                                       |        |
| uint    | 32 位无符号整数类型	0 到 4,294,967,295 | 0                                                       |        |
| ulong   | 64 位无符号整数类型                       | 0 到 18,446,744,073,709,551,615                         | 0      |
| ushort  | 16 位无符号整数类型                       | 0 到 65,535                                             | 0      |

sizeof() :表达式 sizeof(type) 产生以字节为单位存储对象或类型的存储尺寸。

- 引用类型
   【后续补充】
- 指针类型
   【后续补充】

#### C#类型装换

- 隐式类型转换 ： 这些转换是 C# 默认的以安全方式进行的转换, 不会导致数据丢失。例如，从小的整数类型转换为大的整数类型，从派生类转换为基类。
- 显式类型转换 ：显式类型转换，即强制类型转换。显式转换需要强制转换运算符，而且强制转换会造成数据丢失

(int)num :强制转换
 C#默认的(int)是整型int32，不遵循四舍五入，只取整数部分
 string a = “45.21”;
 int.Parse(a); //数字的string可以转换成int，字符不行。会把null报错。
 输出：45
 convert.ToInt32() string转成int32，与Int.parse()不同，它会把null转成0。

| 序号 | 名称       | 方法&描述                                         |
| ---- | ---------- | ------------------------------------------------- |
| 1    | ToBoolea   | 如果可能的话，把类型转换为布尔型。                |
| 2    | ToByte     | 把类型转换为字节类型。                            |
| 3    | ToChar     | 如果可能的话，把类型转换为单个 Unicode 字符类型。 |
| 4    | ToDateTime | 把类型（整数或字符串类型）转换为 日期-时间 结构。 |
| 5    | ToDecimal  | 把浮点型或整数类型转换为十进制类型。              |
| 6    | ToDouble   | 把类型转换为双精度浮点型。                        |
| 7    | ToInt16    | 把类型转换为 16 位整数类型。                      |
| 8    | ToInt32    | 把类型转换为 32 位整数类型。                      |
| 9    | ToInt64    | 把类型转换为 64 位整数类型。                      |
| 10   | ToSbyte    | 把类型转换为有符号字节类型。                      |
| 11   | ToSingle   | 把类型转换为小浮点数类型。                        |
| 12   | ToString   | 把类型转换为字符串类型。                          |
| 13   | ToType     | 把类型转换为指定类型。                            |
| 14   | ToUInt16   | 把类型转换为 16 位无符号整数类型。                |
| 15   | ToUInt32   | 把类型转换为 32 位无符号整数类型。                |
| 16   | ToUInt64   | 把类型转换为 64 位无符号整数类型。                |

#### C#运算符

- 算数运算符
  - 【+】两数相加
  - 【-】两数相减
  - 【*】两数相乘
  - 【/】相除取整，两数相除，结果还是整数
  - 【%】取余
  - 【++】自增
  - 【–】自减
- 逻辑运算符
  - 【&&】逻辑与，A&&B，A和B都非0，返回True，若A为0，则不对B判定，直接结果为False。
  - 【||】逻辑或，A||B，A和B任意有一个非0，则结果为True。
  - 【！】非，取反
- 关系运算符
  - 【】AB，检查A和B是否相等
  - 【！=】A!=B，检查A和B是否不等
  - 【>,<,<=,>=】大于，小于，小于等于，大于等于
- 位运算符
  - 【&】A&B，二进制表示A和B，然后逐位对比，全为1时出1,有0出0
  - 【|】A|B，二进制表示A和B，然后逐位对比，全0出0，有1出1
  - 【^】A ^ B,二进制表示A和B，然后逐为对比，相同出0，不同出1
  - 【~】二进制表示A，然后逐位取反
  - 【<<】二进制表示A，然后逐位左移，A=00111100，A<<2=11110000
  - 【>>】二进制表示A，然后逐位右移，A=00111100，A>>2=00001111

| A    | B    | A & B | A \| B | A ^ B | ~ A  |
| ---- | ---- | ----- | ------ | ----- | ---- |
| 0    | 0    | 0     | 0      | 0     | 1    |
| 0    | 1    | 0     | 1      | 1     | 1    |
| 1    | 1    | 1     | 1      | 0     | 0    |
| 1    | 0    | 0     | 1      | 1     | 0    |

```
A = 0011 1100
B = 0000 1101
A&B = 0000 1100
A|B = 0011 1101
A^B = 0011 0001
~A  = 1100 0011

```

- 赋值运算符
  - 【=】注意区分=和==
- 补充
  - 【x??y】如果有x，则表达式结果为x，如果没有x（x为null），则表达式结果为y
  - 【x?y:z】这里的x只作为判断条件，即x为真表达式就取y值，x为假表达式就取z值

#### C#分支语句

if-else语句
 if-else 嵌套语句
 switch语句
 seitch嵌套语句
 switch()可以用数字判断，也可应用字符串判断
 【x?y : z】也是一种判断

#### C#循环语句

1、for循环 【增强for循环：foreach多用在遍历字典或者集合上】

```
using System;

namespace test_2020
{
   
    class Program
    {
        static void Main(string[] args)
        {
            /* for 循环执行 */
            for (int a = 10; a < 20; a = a + 1)
            {
                Console.WriteLine("a 的值： {0}", a);
            }
            Console.ReadLine();
        }
    }
}

```

2、while循环 【先判断，再循环】

```
using System;

namespace test_2020
{
   
    class Program
    {
        static void Main(string[] args)
        {
            /* 局部变量定义 */
            int a = 10;

            /* while 循环执行 */
            while (a < 20)
            {
                Console.WriteLine("a 的值： {0}", a);
                a++;
            }
            Console.ReadLine();
        }
    }
}

```

3、do-while循环 【先循环一次，在判断】

```
using System;

namespace test_2020
{
   
    class Program
    {
        static void Main(string[] args)
        {
            /* 局部变量定义 */
            int a = 10;

            /* do 循环执行 */
            do
            {
               Console.WriteLine("a 的值： {0}", a);
                a = a + 1;
            } while (a < 20);

            Console.ReadLine();
        }
    }
}

```

4、break和continue
 break 直接退出循环
 continue 退出本次循环（跳过随后一条语句）

#### C#数组

```
初始化：
int[] num = new int[6] //定义int数组长度为6【0 1 2 3 4 5】
int[] num = new int[]{1,2,3} //给定内容1,2，3
int[] num = new int[3]{1,2,3} //[]内是数组长度
int[0] = 1 //数组第一赋值为 1  索引器是从0开始
string str = new string[]{"Hello world"}; //标准写法new一个
string str = {"Hello", "world"};//简写
获取数组的值：
注意索引器是从0开始的，所以要减 1 

访问数组：循环遍历数组每一个值，foreach() 遍历函数
foreach (int j in num ) // num[] 是一个数组
{
   Console.WriteLine(j);
}

```

#### C#方法（函数）

```
命名：驼峰命名，开头字母大写
多个单词拼接所有开头字母大写

函数的参数设置和传参行为
函数的返回值：外部调用的一个反馈

public：公共的
void ：不需要返回值的类型
int ：需要返回值的类型
函数名：

函数参数修饰符：加在参数前
函数--public int test(ref int a ,ref int b ){ }
调用--test(ref int m,ref int n);
【值传递：传副本，引用传递：传地址，相当于C的指针】
1）无修饰符：无修饰符则按照值传递，被调函数将收到原始数据的一个副本。
2）out：输出参数由被调函数的方法赋值，是应用传递，如果被调函数没有给输出的参数赋值，就会出现编译错误。out一般用调用者一次调用就获得多个返回值。
【函数输出方向可以改变原始数据】
3）ref:调用者必须赋初值，并且可以有被调函数重新赋值，引用传递。如果被调函数未能赋值，不会出现编译错误。【共享】
staticb void Main(string[] args)
{
	int i = 2 ;
	int j = 5 ;
	print("i = %d,j = %d\n",i,j);//交换前
	swap(ref i,ref j);  //ref=* //ref使得main函数里的i，j和swap里的p，q共享了相当于指针
	printf("i = %d,j = %d\n",i,j);//交换后
	return 0 ;
}

static void swap(ref int p,ref int q) //接收变量的地址
{
    int t;
    t = p;
    p = q;
	q = t; 
	return;//void函数不需要返回值，这里是写码习惯
 }
 4）ref和out对比：
 out修饰符的参数必须在方法内修改，而ref可以修改也可以不修改
 out在传入参数的时候，参数是局部变量的话，可以不用赋值，因为out一定会对其赋值【可以在传参的时候临时定义一个变量，不必事先定义】
 ref修饰的参数，在实参必须有初始值才能调用，因为ref不会赋值。
 4）params：这个修饰符允许将一组可变的数量的参数作为单独的逻辑参数进行传递，方法只能有一个params修饰符，且必须是修饰方法的最后一个参数。


```

#### C#面向对象基础

面向过程和面向对象
 面向过程：C语言典型
 过程 是早期一种编程概念
 过程 类似于函数，只能执行，没有返回值
 函数 不仅可以执行，还可以返回结果
 面向过程强调 怎么做：
 1）把某一个需求的所有步骤，从头到尾的实现
 2）根据开发需求，将某些功能独立的代码封装成一个个函数
 3）最后完成代码，就是按顺序的调用不同的函数
 特点：
 1）注重步骤与过程，不注重分工
 2）如果需求太复杂，代码就会变得很复杂【维护性差】
 3）复杂的项目，没有固定的套路，难度大

面向对象：
 面向对象强调谁来做：谁就是对象，我们给对象定义
 面向对象是更大的封装，根据职责，在一个对象中封装多个方法
 1）在完成一个需求前，首先确定职责，要做的事（方法）
 2）根据不同的职责确定不同的对象，在对象内封装不同的方法（多个）
 3）最后完成代码，就是顺序（业务顺序）让不同的对象调用不同的方法
 特点：
 1）注重对象的职责，不同的对象不同的职责
 2）更加适合应对复杂的需求变化，是专门对应复杂项目开发，提供的固定的套路
 3）需要在面向过程的基础上，再学习一些面向对象的语法

#### C#的类和对象

1、类和对象时面向编程的两个核心概念：
 1）类：
 类 是一群具有相同特征或者行为的事物的一个统称，是抽象的，不能直接使用。
 类 就相当于的是一张图纸，模板，是负责创建对象的。
 【我们把特征成为属性，把行为称为方法】
 2）对象：
 对象是由类创造出来的一个具体存在，可以直接使用
 由哪一个类创造出来的对象，就拥有哪一个类中定义的 属性 和 方法。
 研发中，现有 类 再有 对象
 3）类和对象的关系：
 类 是模板，对象是根据类这个模板创造出来的现有类再有对象
 类只有一个，但是对象可以有多个—不同的对象之间的属性的具体内容可能不同
 类 中定义了什么属性和方法，对象中就有什么属性和方法，不可能多或者少

2、类的设计：
 在使用面向对象开发前，首先根据需求，确定有哪些类
 类 的三要素
 1）【类名】 这类事物的名称，满足驼峰命名法
 2）【属性】 这类事物有什么样的特征
 3）【方法（函数）】 这类事物具有什么行为

类名的确定：
 名词提炼，分析整个业务的流程，出现的名词，通常就是找到的 类
 属性和方法的确定：
 对象的特征—属性
 对象的行为—方法

类是模板，不能直接使用，需要实例化

3、类和对象的使用：

```
声明类的关键字 class 
【public访问修饰符】

VS2019中 右键添加类
声明属性
C#中属性较为特殊，它既不同于方法，也不同于字段
属性遵循驼峰命名法
属性最常用的书写方法：public int Age {get ; set ;}
get：属性中具有get，则可以获取该属性的值
set：属性中具有set，则可以向属性设置值
get和set还可以扩充

声明方法（函数）

在C#中万物皆对象，对象都是有类型的

实例化：类变成对象的过程
关键字 new 实例化：类变成对象的过程

namespace test_2020
{
    public class Person //加上public，不然默认是隐式类，外部不能访问
    {
        public string Name { get; set; } // 敲prop，点Tab会自动出来
        public int Age { get; set; } //年龄属性
        public int High { get; set; } //身高属性
        static int Id {get;set;}// 静态
        public void Eat()
        {
            MessageBox.Show("我吃过了");
        }

        public void Run()
        {
            MessageBox.Show("我跑了步");
        }
    }
}

调用：
Person per = new Person(); //Person是类型，per是具体的名字，Person()是之前写好的类
per.Eat();
per.Run();
per.Name = "sun";

在实例化的时候也可以直接赋值：
Person per = new Person()
{
Age = 18 , //注意这里是逗号
Name = "sun"
}

```

#### C#访问修饰符

```
public：共有的，所有类都可以访问
private：私有的，当前类内可以访问
protected：受保护的，当前类以及继承他的子类可以访问
internal：内部的，只限于本项目内的访问
protected internal：内部保护访问，只能是本项目内或子类访问

访问约束级别：
父类和子类的修饰符要保持一致
方法的访问修饰符要和方法参数的访问修饰符一致
注：类 的访问级别默认是隐式的，需要加上public才可以外部访问

静态方法，属性：
static ：静态属性和方法的修饰符
静态和属性可以通过类型直接获取，非静态则必须通过实例化的对象多去
例如：
Person.Id = "123456"
但是不能：per.Id

静态类通过static修饰。一般情况下类型不需要是用静态类修饰，只有当类型中存在扩展方法时需要使用到静态类
```

#### C#集合和字典

```
数组的优势：连续存储，索引很快。赋值修改简单
劣势：在数组中间插入很麻烦，在数组声明的时候必须声明长度、大小固定

ArrayList的使用：
ArrayList是.NET Framework提供的用于数据存储和检索的专用类
命名空间是：System.Collections
它的优势：
1）大小按照存储数据动态扩充与收缩
2）在声明时不需要指定固定长度
3）很方便添加，插入，移除
4）内容类型可以不一样【因为使用object类型接收】

ArrayList的劣势，ArrayList在存储数据的时候采用的object类型进行存储的
ArrayList不是类型安全的，使用会出现类型不匹配错误
就算插入了同一类型的数据，使用的时候也需要转化成对应的数据来处理
ArrayList的存储存在 装箱和拆箱操作，性能低下

装箱和拆箱：
【object】是万类之源，所有类都是继承他的
父类可以接受子类的数据，而object是所有类的父类，所以他可以接受任何类型的数据
【装箱】：就是子类的类型通过隐式转换赋给了object类。例如int和string
【拆箱】：就是讲object通过显式转换赋给原来的子类类型，例如赋给int
装箱拆箱会有很多的性能损耗

正式因为ArrarList的缺陷，C#2.0之后出现了 【泛型 】概念。List集合就是这种
【泛型】：限制集合只能存储单一类型数据的一种手段。用<>表示
List<int>,这样这个集合只能接受int型


List集合：
1）list集合与ArrayList继承了相同的接口，故与之类似
2）在声明list集合时，需要同时为其声明list内的类型，例如：
List<int> intList = new List<int>(); //声明list集合
list集合的一些方法
自己写的类可以在list<>中使用吗？可以！
list<Person> perlist = new list<Person>();

字典的声明：
在声明字典的时候，需要同时声明dictionary字典内 键 与 值 的类型
示例：Dictionary<int,string> dictionary = new dictionary<int,string>()
也可以在实例化的时候赋值：
Dictionary<string,string> dictionary = new dictionary<string,string>()
{
  {"A","123"},{"B","456"},{"C","789"}
}
键与键值可以是任何类型，但是键必须唯一，而值可以不唯一

赋值方式：
1）add赋值：如果这个键已经有值了，那么不能修改，会报错
dictionary.add(1,"99分")//1是键 ，不是索引，
2）索引器赋值：如果这个键已经有值了，可以修改，会覆盖掉之前的值
dictionary[1]="88分" //这里[键]，不是下标
3）初始化的时候赋值

获取键对应的值：
1）索引器取值（根据键取值）
string value = dictionary[1] //注意这里前提是dictionary值的类型是string
2）foreach遍历取值

bool b = dictionary.Remove(1) //Remove(1)删除键为1的值，删除后返回为布尔类型，删除成功返回True失败False


注意：键key与值value可以是任何类型，但是key是唯一的，value可以不唯一
使用add()方法添加键值对时，不可添加已有的键名
索引模式可以新赋值，也可以修改已有的键值，索引器内写的是键key，不是下标


【foreach的使用】：
foreach就是对增强循环
foreach对遍历字典或者集合具有天然的优势

操作数组：
int[] ints = {1,2,34,5,6};
foreach(int item in ints)
{
  //每次循环，其item都是数组中一个元素
}

操作集合：
List<int> intList = new List<int>();
foreach(int item in intList)
{
	//每次循环，item都是List集合中一个元素
}

操作字典：
KeyValuePair<string,string> :键值对专用【字典就是键值对类型】
foreach(KeyValuePair<string,string> item in dictionary)
{
	string key = item.key;
	string value = item.Value;
}



```

by 久违 2020.3.20