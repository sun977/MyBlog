### C#学习笔记整理【二】



### 目录

- - - [C#学习笔记整理【二】](https://blog.csdn.net/weixin_42742658/article/details/105474345#C_0)

    - - [1、C#内置引用类型](https://blog.csdn.net/weixin_42742658/article/details/105474345#1C_2)

      - [2、C#运算符：](https://blog.csdn.net/weixin_42742658/article/details/105474345#2C_30)

      - [3、数据类型转换:](https://blog.csdn.net/weixin_42742658/article/details/105474345#3_53)

      - [4、装箱和拆箱：](https://blog.csdn.net/weixin_42742658/article/details/105474345#4_64)

      - [5、goto语句：](https://blog.csdn.net/weixin_42742658/article/details/105474345#5goto_68)

      - [6、数组：数组也是对象【C#内万物皆对象】](https://blog.csdn.net/weixin_42742658/article/details/105474345#6C_126)

      - - [1）定义：](https://blog.csdn.net/weixin_42742658/article/details/105474345#1_131)
        - [2）数组定义的三种方式：](https://blog.csdn.net/weixin_42742658/article/details/105474345#2_141)
        - [3）遍历数组：](https://blog.csdn.net/weixin_42742658/article/details/105474345#3_146)
        - [4）多维数组：](https://blog.csdn.net/weixin_42742658/article/details/105474345#4_162)
        - [5）交错数组：](https://blog.csdn.net/weixin_42742658/article/details/105474345#5_205)
        - [6）数组是引用类型：](https://blog.csdn.net/weixin_42742658/article/details/105474345#6_253)
        - [7）隐式类型的数组：](https://blog.csdn.net/weixin_42742658/article/details/105474345#7_264)

      - [7、方法的概念：](https://blog.csdn.net/weixin_42742658/article/details/105474345#7_280)

      - - [1）方法的定义：](https://blog.csdn.net/weixin_42742658/article/details/105474345#1_299)
        - [2）Main函数：](https://blog.csdn.net/weixin_42742658/article/details/105474345#2Main_306)
        - [3）静态类：](https://blog.csdn.net/weixin_42742658/article/details/105474345#3_312)
        - [4）静态方法和实例方法（定义和调用）：](https://blog.csdn.net/weixin_42742658/article/details/105474345#4_319)
        - [5）实例化](https://blog.csdn.net/weixin_42742658/article/details/105474345#5_327)

      - [8、方法（函数）重载：](https://blog.csdn.net/weixin_42742658/article/details/105474345#8_335)

      - - [1）函数参数的默认值：【必须放在参数列表的最后】](https://blog.csdn.net/weixin_42742658/article/details/105474345#1_345)
        - [2）函数的嵌套调用：](https://blog.csdn.net/weixin_42742658/article/details/105474345#2_353)
        - [3）函数的递归调用：](https://blog.csdn.net/weixin_42742658/article/details/105474345#3_357)
        - [4）外部函数的调用：【extern】](https://blog.csdn.net/weixin_42742658/article/details/105474345#4extern_372)

      - [9、类和对象 C#学习笔记整理【三】](https://blog.csdn.net/weixin_42742658/article/details/105474345#9_C_397)



#### 1、C#内置引用类型

- 1）dynamic类型：
- 2）object类型：（对象类型）
   object类型在.NET  Framework中是Object的别名。在C#的系统中。所有的类型（预定类型，用户类型，引用类型和值类型）都是直接或者间接从Object类型继承的。可以接受任何类型的赋值。装箱：值类型变量转换为object类型的过程。拆箱：将object类型变量转换为值类型的过程。装箱和拆箱十分消耗资源。【对象时引用类型】
- 3）string类型：
   string类型是一个字符序列（零个或者更多unicode字符），string是从,NET Framework中String的别名。
   尽管string是一个引用类型，但是定义相等运算符（==和！=）是为了比较string对象的值（而不是引用）。这使得对字符串的相等性的测试更为直观。

```
string a = "Hello";
string b = "H";
b = b+a;
Console.WriteLine(a==b); //显示True
Console.WriteLine((object)a==(object)b);//显示Fals
string c = "Hello" + "world";  //字符串拼
string d = "test";
char x = d[2]
Console.WriteLine(x) //显示"s"，字符串切片
string str = "\\u0066\n"
string path = @"c:\test\test_2020.txt";  //表示路径方法一
string path = "c:\\test\\test_2020.txt";  //表示路径方法
string m = "Hello";
string n = String.Copy(m);//复制m的值给n
string h = "Hello";
Console.WriteLine(m == n); //返回True
Console.WriteLine((object)m ==(object)n); //返回False，后一个(object)n是实例，而不是对象，所以不相等
Console.WriteLine((object)m == (object)h); //返回True
```

#### 2、C#运算符：

```
x.y 成员访问
f(x) 函数调用
a[i] 索引器索引
new 类型实例化
typedef 返回表示操作数的 System.Type对象
checked 对整数运算启用溢出检查【检测异常】
checked
{
   // 需要检测的代码
}
unchecked 对整数运算禁用溢出检查，这是编译器默认的行为【不检测异常】
unchecked
{
   // 不需要检查的代码
}
default(T) 返回类型T的默认初始化值，T为引用类型时返回null，T为值类型时返回0，T为结构体的时返回填充0挥着null的成员。

delegate 声明并返回一个委托
sizeof  返回操作数大小（以字节为单位）
```

#### 3、数据类型转换:

1）自动转换：隐式转换，安全的转换，自动进行
 2）强制转换：显示转换
 3）使用System.Convert类
 4）使用Parse方法
 5）as
 6）is
 由于对象是多态的，因此基类类型的变量可以保存派生类型。若要访问派生类型的方法，需要将值强制转换回派生类型。不过在这种情况下，如果只尝试简单的强制转换，会导致引发Invalid
 CastException的风险。这就是C#提供is和as运算符的原因。你可以使用这两个运算符来测试强制转换是否会成功，而没有引发风险。通常as运算符更高效一些，因为如果强制转换成功，它会返回强制转换值。而is是指返回一个布尔值。因为只想确定对象的类型，而无需对他进行强制转换的话，可以使用is运算符。

#### 4、装箱和拆箱：

- 装箱：将值类型转换为引用类型
- 拆箱：将引用类型转换为值类型

#### 5、goto语句：

goto语句是将程序控制语句直接传给标记语句（跳转）
 goto的一个通常用法是将控制传递给特定的switch-case标签huoswitch语句中的默认标签。
 goto语句还用于跳出深层嵌套循环

```
举例：
using System;

namespace test_2020_2
{
    class Program
    {
        static void Main(string[] args)
        {
            
			int x = 200;
			int y = 4;
			int conut = 0;
			string[,] array = new string[x, y];// 定义一个二维数组

			for (int i = 0; i < x; i++)
			{
				for (int j = 0; j < y; j++)
				{
					array[i,j] = (++conut).ToString();
				}
			}

			Console.WriteLine("Enter the Number to search for :");
			string myNumber = Console.ReadLine(); //接收读进的一个数

			for (int i = 0; i < x; i++)
			{
				for (int j = 0; j < y; j++)
				{
					if (array[i,j].Equals(myNumber))
					{
						goto Fonud; //这里定义一个Found标签，找到了就执行标签的代码
					}

				}
			}

			Console.WriteLine("The number {0} was not fonud.", myNumber);
			goto Finish;

		Fonud://标签
		Console.WriteLine("The number {0} is fonud.", myNumber);

		Finish:
		Console.WriteLine("End of Search.");



		}
	}
}
```

#### 6、数组：数组也是对象【C#内万物皆对象】

- 一维数组
- 多维数组
- 交叉数组

##### 1）定义：

数组是存储相同类型元素的固定的顺序集合。是同一类型变量的集合。
 数组中每个指定的元素是通过索引来访问的。
 注：
 1）在C#中，值类型数组所有元素默认值为0，引用类型数组的默认值为null
 2）数组本身是引用类型
 3）数组固定大小
 4）所有的数据连续存储在一起。
 5）所有的数组都是由连续的内存组成。

##### 2）数组定义的三种方式：

1）数组类型[] 数组名 = new 数组类型[元素个数];
 2）数组类型[] 数组名 = new 数组类型[]{数组初始化列表};
 3）数组类型[] 数组名 = {数组初始化列表};

##### 3）遍历数组：

```
string[] names = {"sun","Tom","Jery"};
//for循环遍历
for (int i = 0;i<names.Length;i++)
{
	Console.WriteLine("My name is {0}",names[i])
}
//foreach遍历
foreach(string name in names)
{
	Console.WriteLine("My name is {0}",name);
}

Array是所有数组类型的基类。Array提供了很多的方法和属性，用于排序，搜索和复制等等。
```

##### 4）多维数组：

```
int[,] data = new int[2,3]//定义2行3列的数组
    0    1    2
0   00   01   02
1   10   11   12
2   20   21   22

int[,,] data = new int[4,2,3]//定义三维数组

实例化：
int[,] data = new int[,]
{
	{1,2},//一个花括号一行
	{3,4},
	{5,6},
	{7,8}
};//这是一个4行2列的数组

string[,] data = new string[3,2]
{
	{"one","two"},
	{"three","four"},
	{"five","six"}
};

int[,,] data3D = new int[,,] //高2行2列3的数组
{
	{
		{1,2,3},
		{4,5,6}
	},
	{
		{7,8,9},
		{10,11,12}
	}
};

int[,,] data3D = new int[2,2,3] 
{
	{{1,2,3},{4,5,6}},{{7,8,9},{10,11,12}}
};
```

##### 5）交错数组：

交错数组是元素为数组的数组。交错数组元素的维度和大小可以不同。交错数组有时也叫“数组的数组”。

```
int[][] jadata = new int[3][];

jadata[0] = new int[5];
jadata[1] = new int[4];
jadata[2] = new int[3]; 

多维数组和交错数组的区别：
1）多维数组的每一行元素个个数是一样的，数组的长度为数组所有元素的个数。
2）交错数组的每一行可以是不同的，数组的长度为第一维数组的元素个数。

params 当传进参数长度可变的时候用这个修饰
Array.Reverse(); // 逆序

可变参数的数组
举例：
using System;

namespace test_2020_2
{
    class Program
    {

		class ParamArray
		{
			public int AddElements(params int[] arr)//params 当传进参数长度可变的时候用这个修饰
			{
				int sum = 0;
				foreach (int i in arr)
				{
					sum += i;
				}
				return sum;
			}
		}

		static void Main(string[] args)
		{
			ParamArray add = new ParamArray();
			int sum = add.AddElements(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
			Console.WriteLine("总和：{0}", sum);

		}
	}
}
```

##### 6）数组是引用类型：

| 类型名   |              |                                                        |
| -------- | ------------ | ------------------------------------------------------ |
| 值类型   | 基本数据类型 | int，long，float，char，bool                           |
|          | 枚举类型     | 枚举：enum                                             |
|          | 结构类型     | 结构：struct                                           |
| 引用类型 | 类           | 基类：System.Object，字符串：string，自定义的类：class |
|          | 接口         | 接口：interface                                        |
|          | 数组         | 数组：int[],string[]                                   |

##### 7）隐式类型的数组：

```
var a = new[]{1,2,3,4};
var b = new[]{"sun","Tom",null};//var倒是是什么类型系统会根据后面的内容自己判定
var c = new[]
{
	new[]{1,2,3,4},
	new[]{5,6,7,8}
};
var d = new[]
{
	new[]{"Mon","sun","Lucky","Dva"},
	new[]{"Tom","Suma","Frank"}
};
```

#### 7、方法的概念：

函数：C,C++等里面的概念
 方法：写在类里面的函数
 方法只能写在类里面，不能写在命名空间里面

函数就是一堆代码进行重用的一种机制。函数就是一段代码，这个代码有可能有输入的值，可能返回值。

```
以上已经出现的方法总结：
Console.Write();
Console.WriteLine();
Console.ReadLine();
Console.ReadKey();
int.Parse(string);
Convert.ToInt32(string);
```

对于有static修饰的方法，使用： 类名.方法()  调用
 如果在类中调用自己的由static修饰的方法，可以省略类名

##### 1）方法的定义：

```
[访问修饰符][static] 返回值类型 方法名()
{
	方法体;
}
```

##### 2）Main函数：

static 表示方法是静态的，就是说方法在程序被编译的时候就被分配了内存，使用时候不用生成某个类的对象，直到程序退出才释放。
 void 表示方法没有返回值，没有return
 main 是方法名，这个方法是特殊的。是Main()就是主函数，程序的入口
 static 与 auto 是对应的，一般没有写static的方法默认都是auto，只不过auto不需要写出来

##### 3）静态类：

用 static 修饰的类成为静态类，这个类里面的方法都是静态的，非静态的方法在里面是不可以使用的。

静态变量，静态方法，静态类，都不能使用new关键字创建静态的实例。
 静态成员变量是和类相关联的，可以作为类中’共’有的变量，不依赖于特定的对象和实例，访问的时候通过： 类名.方法() 的方式

##### 4）静态方法和实例方法（定义和调用）：

静态
 static 关键字
 使用类名调用
 在静态方法中，可以访问静态成员
 在静态方法中，不可以直接访问实例成员
 调用前初始化

##### 5）实例化

不需要 static 关键字
 使用实例对象调用 （new一个）
 在实例方法中，可以直接访问静态成员
 在实例方法中，可以直接访问实例成员
 实例化对象时初始化

#### 8、方法（函数）重载：

方法名相同，但是参数类型或者参数个数不同，与返回值无关，这就是方法重载
 方法重名：方法名和参数类型个数等都相同
 方法重载是指同样的方法有多种不同的实现方法。
 方法重载是在一个类中两次或者多次定义同名的方法，但是方法的参数类型或个数不同。
 静态成员方法不能重载

方法相同，参数类型个数相同，但是return返回值不同，这也不构成重载

##### 1）函数参数的默认值：【必须放在参数列表的最后】

```
static void Print(string name , int age=18)//只能放在最后
{
	Console.WriteLine("Name:{0},Age:{0}",name,age);
}
```

##### 2）函数的嵌套调用：

函数的定义是相互平行的，独立的。在定义函数的时候一个函数不能包括另一个函数。
 不能嵌套定义函数，但是可以嵌套调用函数。

##### 3）函数的递归调用：

在调用函数的时候又出现函数本身【自己调用自己】，有直接递归调用和间接递归调用。

```
举例：
public static void Main(string[] args)
{
	Faction();
}

static void Faction()
{
	Console.WriteLine("恭喜恭喜")
	Faction();
}
```

##### 4）外部函数的调用：【extern】

C#中使用 extern 修饰来声明在外部实现的方法，常用系统API函数来调用。
 extern 修饰符常见用法实在使用Interop服务调入非托管代码时与DLLIMmport属性一起使用，在这种情况下，该方法必须声明为 static
 [DLLImport(“avifil32.dll”)]
 private static extern void AVIFilelnit();

```
举例：
namespace test-2020
{
	class Program
	{
		[DLLImport("User32.dll",CharSet = CharSet.Unicode)] //引用动态链接库，选定字符集
		public static extern int MessageBox(IntPtr h ,string m ,string c ,int type);
		static int Main(string[] args)
		{
			string myString;
			Console.Write("Enter your message: ");
			myString = Console.ReadLine();
			return MessageBox((IntPtr)0,myString,"My Message Box",0);//外部调用
		}

	}
}

```

#### 9、类和对象 C#学习笔记整理【三】

by 久违 2020.3月