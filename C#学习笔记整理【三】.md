### C#学习笔记整理【三】



### 目录

- - - [C#学习笔记整理【三】](https://blog.csdn.net/weixin_42742658/article/details/105474803#C_0)

    - - [9、类和对象](https://blog.csdn.net/weixin_42742658/article/details/105474803#9_3)

      - - [1）类和对象的关系](https://blog.csdn.net/weixin_42742658/article/details/105474803#1_5)

        - [2）类和结构体：](https://blog.csdn.net/weixin_42742658/article/details/105474803#2_8)

        - [3）面向对象的特性：](https://blog.csdn.net/weixin_42742658/article/details/105474803#3_16)

        - [4）类的实例化：](https://blog.csdn.net/weixin_42742658/article/details/105474803#4_21)

        - [5）类成员的访问：](https://blog.csdn.net/weixin_42742658/article/details/105474803#5_25)

        - [6）类的属性：](https://blog.csdn.net/weixin_42742658/article/details/105474803#6_34)

        - [7）C#中结构体的特点：](https://blog.csdn.net/weixin_42742658/article/details/105474803#7C_142)

        - [8）C#构造函数和析构函数：](https://blog.csdn.net/weixin_42742658/article/details/105474803#8C_153)

        - [9）类的构造方法：](https://blog.csdn.net/weixin_42742658/article/details/105474803#9_163)

        - - [类的构造方法（构造函数）：](https://blog.csdn.net/weixin_42742658/article/details/105474803#_164)
          - [类的析构方法（析构函数）：](https://blog.csdn.net/weixin_42742658/article/details/105474803#_171)

        - [10）类的继承：](https://blog.csdn.net/weixin_42742658/article/details/105474803#10_178)

        - [11）静态构造函数：](https://blog.csdn.net/weixin_42742658/article/details/105474803#11_384)

        - - [静态构造函数注意点：](https://blog.csdn.net/weixin_42742658/article/details/105474803#_387)

        - [12）析构函数：](https://blog.csdn.net/weixin_42742658/article/details/105474803#12_396)

        - [13）类中的常量：【const 和 readonly】](https://blog.csdn.net/weixin_42742658/article/details/105474803#13const__readonly_449)

        - [14）类的嵌套：](https://blog.csdn.net/weixin_42742658/article/details/105474803#14_465)

        - [15）类的析构方法：](https://blog.csdn.net/weixin_42742658/article/details/105474803#15_503)

        - [16）关于重载,重写,覆写：](https://blog.csdn.net/weixin_42742658/article/details/105474803#16_555)

        - - [1）重写 override：](https://blog.csdn.net/weixin_42742658/article/details/105474803#1_override_558)
          - [2）重载 overload：](https://blog.csdn.net/weixin_42742658/article/details/105474803#2_overload_571)
          - [3）覆写 new：](https://blog.csdn.net/weixin_42742658/article/details/105474803#3_new_578)

        - [17）抽象类：](https://blog.csdn.net/weixin_42742658/article/details/105474803#17_659)

        - - [关键字 ： abstract](https://blog.csdn.net/weixin_42742658/article/details/105474803#__abstract_660)
          - [抽象方法的特性：](https://blog.csdn.net/weixin_42742658/article/details/105474803#_674)
          - [抽象属性：](https://blog.csdn.net/weixin_42742658/article/details/105474803#_685)

        - [18）类的修饰符：](https://blog.csdn.net/weixin_42742658/article/details/105474803#18_845)

        - [19）集合类：](https://blog.csdn.net/weixin_42742658/article/details/105474803#19_853)

        - - [ArrayList类:](https://blog.csdn.net/weixin_42742658/article/details/105474803#ArrayList_861)
          - [Queue类](https://blog.csdn.net/weixin_42742658/article/details/105474803#Queue_877)
          - [stack类](https://blog.csdn.net/weixin_42742658/article/details/105474803#stack_883)
          - [HashTable类](https://blog.csdn.net/weixin_42742658/article/details/105474803#HashTable_886)
          - [SortLedist类](https://blog.csdn.net/weixin_42742658/article/details/105474803#SortLedist_923)
          - [Dictionary类](https://blog.csdn.net/weixin_42742658/article/details/105474803#Dictionary_959)

        - [20）字符串String类：](https://blog.csdn.net/weixin_42742658/article/details/105474803#20String_1119)



#### 9、类和对象

##### 1）类和对象的关系

类是对象的模板，对象是类的具体实现。

##### 2）类和结构体：

- 1）类和结构是.NET Framework中的常规类型的两种基本构造。两者在本质上都属于数据结构，封装着一组整体作为一个逻辑单位的数据和行为。数据和行为是该类或结构体的“成员”，它们包含各自的方法，属性和事件等。
- 2）类或者结构体相当于蓝图，用于在运行时创建实例或对象。【实例化】
- 3）类 是一种 引用类型 。
- 4）结构体是一种 值类型 。
- 5）类通常用于较为复杂的行为建模，或者要在创建对象后进行修改的数据建模。结构体最适合一些小型的数据结构，这些结构包含的数据以创建后不修改为主。
- 6）类与结构体不同，类支持继承和多态，是面向对象编程的一个基本特点

##### 3）面向对象的特性：

- 1）封装
- 2）继承
- 3）多态

##### 4）类的实例化：

关键字：new
 类 实例名 = new 类();

##### 5）类成员的访问：

实例名.方法名()
 实例名.属性

字段，方法和属性都类的成员，他们需要定义访问级别。访问级别的用处在控制成员在那些地方可以被访问，这样可以达到面向对象中“封装”的目的

访问修饰符： public,private,internal,protected等
 类默认为：internal，类成员默认为：private

##### 6）类的属性：

字段用 public 修饰
 属性的定义 get和set
 属性是为了保护与之相应的字段，保证字段的读取和赋值符合要求
 属性可以分为：读写，只读，只写
 只定义 get 就是只读
 只定义 set 就是只写
 定义 get和set 就是读写

```
举例1：结构体
using System;
using System.Text;
     
struct Books   //声明结构体
{
   public string title;
   public string author;
   public string subject;
   public int book_id;
};  

public class test_2020
{
   public static void Main(string[] args)
   {

      Books Book1 = new Book();        //声明 Book1，类型为 Book 
      Books Book2 = new Book();        //声明 Book2，类型为 Book 

      /* book 1 详述 */
      Book1.title = "C Programming";
      Book1.author = "Nuha Ali";
      Book1.subject = "C Programming Tutorial";
      Book1.book_id = 6495407;

      /* book 2 详述 */
      Book2.title = "Telecom Billing";
      Book2.author = "Zara Ali";
      Book2.subject = "Telecom Billing Tutorial";
      Book2.book_id = 6495700;

      /* 打印 Book1 信息 */
      Console.WriteLine("Book 1 title : {0}", Book1.title);
      Console.WriteLine("Book 1 author : {0}", Book1.author);
      Console.WriteLine("Book 1 subject : {0}", Book1.subject);
      Console.WriteLine("Book 1 book_id :{0}", Book1.book_id);

      /* 打印 Book2 信息 */
      Console.WriteLine("Book 2 title : {0}", Book2.title);
      Console.WriteLine("Book 2 author : {0}", Book2.author);
      Console.WriteLine("Book 2 subject : {0}", Book2.subject);
      Console.WriteLine("Book 2 book_id : {0}", Book2.book_id);      

      Console.ReadKey();
      //Console.ReadLine(); 会等待直到用户按下知回车，道一次读入一行
      //Console.ReadKey(); 则是等待用户按下任意键，一次读入一个字符内。

   }
}

举例2：结构体
using System;
using System.Text;
     
struct Books   //声明结构体,结构体内也可以声明方法
{
   private string title;
   private string author;
   private string subject;
   private int book_id;

   public void getValue(string t,string a,string s,int id)
   {
   	title = t;
   	author = a;
   	subject = s;
   	book_id = id;
   }

   public void ShowInfo()
   {
   	Console.WriteLine("title:{0}",title);
   	Console.WriteLine("author:{0}",author);
   	Console.WriteLine("subject:{0}",subject);
   	Console.WriteLine("book_id:{0}",book_id);
   }

};  

public class test_2020
{
   public static void Main(string[] args)
   {

      Books Book1 = new Book();        //声明 Book1，类型为 Book 
      Books Book2 = new Book();        //声明 Book2，类型为 Book 

      Book1.getValue("C Programming","Nuha Ali","C Programming Tutorial","6495407");
      Book2.getValue("Telecom Billing","Zara Ali","Telecom Billing Tutorial","6495700");

      Book1.ShowInfo(); //打印
      Book2.ShowInfo();     

   }
}
```

##### 7）C#中结构体的特点：

- 1）结构体可以带有方法，字段，索引，运算方法和事件
- 2）结构体可以定义构造函数，但是不能定义析构函数。不能为结构体定义默认的构造函数。默认的构造函数是自动定义的，且不能改变。
- 3）与类不同，结构体不能继承其他类或者结构体
- 4）结构体不能视为其他类或者结构体的基础结构
- 5）结构体可以实现一个或多个接口
- 6）结构体成员不能指定为：abstract,virtual,protected
- 7）当使用new创建一个结构体时，会调用适当的构造函数来创造结构【不会被实例化】。与 类 不同，类在new的时候已经实例化了。
- 8）如果不适用new操作，只有在结构体内的所有成员字段都初始化之后，对象才能使用。

##### 8）C#构造函数和析构函数：

C# 中的构造函数：【生】
 类的 构造函数 是类的一个特殊的成员函数，当创建类的新对象时执行。
 构造函数的名称与类的名称完全相同，它没有任何返回类型。

C# 中的析构函数：【死】
 类的 析构函数 是类的一个特殊的成员函数，当类的对象超出范围时执行。
 析构函数的名称是在类的名称前加上一个波浪形（~）作为前缀，它不返回值，也不带任何参数。
 析构函数用于在结束程序（比如关闭文件、释放内存等）之前释放资源。析构函数不能继承或重载。

##### 9）类的构造方法：

###### 类的构造方法（构造函数）：

1）构造方法用来创建对象，并且可以在创建对象中，对对象进行初始化
 2）构造方法是用来创建对象的特殊方法，方法名和类名一样，没有返回值，连 void 都不用。
 3）构造方法可以有参数，new 对象的时候传参即可。
 4）如果不指定构造函数，则类有一个默认的无参构造函数。如果指定了构造函数，则不再用默认的构造函数，如果需要无参构造函数，可以自己写
 5）构造函数可以重载，也就是多个参数不同的构造函数

###### 类的析构方法（析构函数）：

1）不能在结构体中定义析构函数，只能对类使用析构函数
 2）一个类只能有一个析构函数
 3）析构函数无法继承或者重载
 4）无法调用析构函数，它们是自动被调用的
 5）析构函数没有修饰符，也没有参数

##### 10）类的继承：

```
<访问修饰符符> class <基类>
{
 ...
}
class <派生类> : <基类>
{
 ...
}


举例1：类实例
public class Person
{
	public string Name {get;set;}
	public int Age {get;set;}

	public Person(string name,int age) // 构造函数 【名称与类名一样】
	{
		Name = name;//如果参数一样的话，一般用this.name = name;
		Age = age;
	}
};

class Program
{
	static void Main(string[] args)
	{
		Person person1 = new Person("Sun",18);//实例化的时候初始化
		Console.WriteLine($"person1 name:{person1.Name},Age:{person1.age}");//注意 $ 的使用

        Person person2 = person1;
        person2.Name = "Tom";//重新赋值name
        person2.Age = "6";//重新赋值Age
        //这里重新赋值之后，person1的Name和Age也会被改掉，因为类是引用类型

        Console.WriteLine("person2 name:{0},age:{1}",person2.Name,person2.Age);
        Console.WriteLine("person1 name:{0},age:{1}",person1.Name,person1.Age);
	}
}

运行上述代码后输出：
person1 name:Sun , age:18
person2 name:Tom , age:6
person1 name:Tom , age:6


举例2：类实例
using System;
using System.Collections.Generic;
using System.Text;

namespace test_2020_2
{
    public class CalenderEntry
    {
        private DateTime date;//字段：类或者结构体中直接声明的任意类型的变量 field
        public string day;

        public DateTime Date
        {
            get { return date; }//get访问器

            set//set访问器
            {   //对年份的范围进行设置
                if (value.Year > 1900 && value.Year <= DateTime.Today.Year)
                {
                    date = value;
                }
                else
                {
                    throw new ArgumentOutOfRangeException();//抛出异常
                }
            }
        }

        public void SetData(string dateString)
        {
            DateTime dt = Convert.ToDateTime(dateString);

            if (dt.Year > 1900 && date.Year <= DateTime.Today.Year)
            {
                date = dt;
            }
            else
            {
                throw new ArgumentOutOfRangeException();//抛出异常
            }
        }

        public TimeSpan GetTimeSpan(string dateString)
        {
            DateTime dt = Convert.ToDateTime(dateString);
            if (dt != null && dt.Ticks < date.Ticks)
            {
                return date - dt;
            }
            else
            {
                throw new ArgumentOutOfRangeException();//抛出异常
            }
        }
    }
    
    class Program
    {
    	static void Main(string[] args)
    	{
    		CalenderEntry birthday = new CalenderEntry();//实例化
			birthday.day = "Saturday";
    	}
    }
}

举例3：类实例
using System;
using System.Collections.Generic;
using System.Text;

namespace test_2020_2
{
	public class Person
	{
		private string firstName;
		private string lastName;

		public Person(string first,string last)//构造函数
		{
			firstName = first;
			lastName = last;
		}
        
        public string Name => $"{firstName} {lastName}";
        // => 符号用于属性赋值或属性中检索值的表达式，表达式的主体定义
	}

	class Program
	{
		static viod Main(string[] args)
		{
			var person = new Person("Sun","Tom");
			Console.WriteLine(person.Name);
		}
	}
}

举例4：类实例
using System;
using System.Collections.Generic;
using System.Text;

namespace test_2020_2
{
	public class SaleItem
	{
		string name;
		decimal cost;

		public SaleItem(string name , decimal cost)
		{
			this.name = name;//重名的时候用this代指，区分用的
			this.cost = cost;
		}

		public string Name
		{
			get => name;
			set => name = value;// => 在C#7.0之后可以使用【vs2017之后】
		}

		public decimal Price
		{
			get => cost;//之前都是使用return
			set => cost = value;
		}
	}

	class Program
	{
		static viod Main(string[] args)
		{
			var item = new SaleItem("Shoes",19.95m);
			Console.WriteLine($"{item.name}:sell for {item.Price}");
		}
	}
}

不同写法：
1）
get 
{
	return name;
}
set
{
	name = value;
}

2）
get => name;
set => name = value;
两种写法效果一样
```

##### 11）静态构造函数：

静态构造函数是C#的一个新特性，一般在初始化一些静态变量的时候用到它。这个构造函数是属于类的，而不是类的实例的，就是说这个构造函数只会被执行一次。也就是在创建第一个实例或者引用任何静态成员之前，由编译系统自动完成。

###### 静态构造函数注意点：

- 1）静态构造函数既没有访问修饰符，也没有参数。因为是编译系统调用的，所以public和private等就没有意义了。
- 2）在创建一个类实例或者任何静态成员被引用时，编译系统会自动调用静态构造函数来初始化类，也就是说我们无法直接调用静态构造函数，也无法控制什么时候执行静态构造函数。
- 3）一个类只能有一个静态构造函数
- 4）静态构造函数最多只运行一次
- 5）静态构造函数不可以被继承
- 6）一个类可以同时拥有实例构造函数和静态构造函数，这是唯一可以具有相同参数列表的同名方法共存的情况。

##### 12）析构函数：

1）和构造函数不同的是，析构函数在类撤销的时侯运行，常用来处理类用完之后的收尾工作。由于类一旦撤销就将不存在，因此所说的收尾工作主要是对象在运行过程中动态申请内存的回收工作。析构函数不能带有参数，不能带有修饰符，不能显示的被调用，一个对象的析构函数在这个对象被撤销的时候自动调用。
 2）析构函数不能被继承，不能显示调用，如果类没有析构函数，编译器会自动调用默认的析构函数，如果类有析构函数则需要我们来完成内存的回收和类的退出的各种操作。

变量私有化，方法公有化
 private 变量
 public 方法()

```
举例：析构函数
using System;
using System.Collections.Generic;
using System.Text;

namespace test_2020_2
{
	public class Line
	{
		private double length;

		public Line()
		{
			Console.WriteLine("对象已经创建。");
		}

		~Line() //析构函数 [对象结束的时候调用]
		{
			Console.WriteLine("对象已删除。");
		}
    
        public void setLength(double len)
        {
        	length = len;
        }

        public double getLength()
        {
        	return length;
        }

	}

	class Program
	{
		static viod Main(string[] args)
		{
			Line line = new Line();
            line.setLength(6.0);
            Console.WriteLine(line.getLength());
		}
	}
}
```

##### 13）类中的常量：【const 和 readonly】

```
class Calendar
{
	const int months = 12;
	const int weeks = 52;
	const int days = 365;
	const double daysPerWeek = (double)days / (double)weeks;
	const double daysPerMonth = (double)days / (double)months;
};

readonly 只读不可以更改
```

##### 14）类的嵌套：

```
举例：
using System;
using System.Collections.Generic;
using System.Text;

namespace test_2020_2
{
	public class Container
	{
		public class Nested //类里面套类
		{
			private Container parent;

			public Nested
			{
				//构造函数
			}

			public Nested(Container parent)// 构造函数 【重载】
			{
				this.parent = parent;
			}
		}
	}

	class Program
	{
		static viod Main(string[] args)
		{
            Container.Nested nest = new Container.Nested();
            //嵌套类的实例化
		}
	}
}
```

##### 15）类的析构方法：

抽象方法不能加{}，只能在子类中实现

```
using System;
using System.Collections.Generic;
using System.Text;

namespace test_2020_2
{
	//方法的签名
	abstract class Motorcycle // abstract 抽象类 【摩托车】
	{
		public void StartEngine() //公共类型的方法
		{}

		protected void AddGas(int gallons)//保护类型的方法
		{}
        
        public virtual int Drive(int miles,int speed)// 虚拟方法
        {
        	return 1 ;
        }

        public abstract double GetTopSpeed();//抽象方法，不能加{}，只能在子类中实现
	};

    class TestMotorcycle : Motorcycle //继承父类
    {
    	public override double GetTopSpeed()//override重写
    	{
    		return 120.8;
    	}
    }

	class Program
	{
		static viod Main(string[] args)
		{
           TestMotorcycle moto = new TestMotorcycle();

           moto.StartEngine();
           moto.AddGas(15);
           moto.Drive(5,20);

           double speed = moto.GetTopSpeed();
           Console.WriteLine("我的最高速度是{0}",speed);
		}
	}
}


```

##### 16）关于重载,重写,覆写：

重载、重写、覆写，分别指的是overload、override、new。

###### 1）重写 override：

override重写，是在子类中重写父类中的方法，两个函数的函数特征（函数名、参数类型与个数）相同。用于扩展或修改继承的方法、属性、索引器或事件的抽象或虚拟实现。提供从基类继承的成员的新实现，而通过override声明重写的方法称为基方法。
 【要扩展或者修改继承的方法，属性，索引器或者事件的抽象(abstract)或虚拟(virtual)，必须使用override】
 注意事项：
 1）重写基方法必须具有与override方法相同的签名。
 2）override声明不能更改virtual方法的可访问性，且override方法与virtual方法必须具有相同级别访问修饰符。
 3）不能用new、static、virtual修饰符修改override方法。
 4）重写属性声明必须指定与继承的属性完全相同的访问修饰符、类型和名称。
 5）重写的属性必须是virtual、abstract或override。
 6）不能重写非虚方法或静态方法。
 7）父类中有abstract，那么子类同名方法必定有override，若父类中有 virtual方法，子类同名方法不一定是override，可能是overload。
 8）override必定有父子类关系。

###### 2）重载 overload：

overload重载，在同一个类中方法名相同、参数或返回值不同的多个方法即为方法重载。
 注意事项：
 1）出现在同一个类中。
 2）参数列表不同或返回类型和参数列表都不同，只有返回类型不同不能重载。(参数列表包括参数个数和参数类型)

###### 3）覆写 new：

overwrite覆写，用new实现。在子类中用 new 关键字修饰定义的与父类中同名的方法，也称为覆盖，覆盖不会改变父类方法的功能。

```
举例：
class Parent //父类
{
    public void F() //公开方法
    {
        Console.WriteLine("Parent.F()");
    }

    public virtual void G() //公开虚拟方法
    {
        Console.WriteLine("Parent.G()");
    }

    public abstract double H();//公开抽象方法，抽象方法不能加{}，只能在子类中实现

    public int Add(int x, int y)
    {
        return x + y;
    }

    public float Add(float x, float y) //重载(overload)Add函数
    {
        return x + y;
    }
}

class Child1:Parent //子类一继承父类
{
    new public void F() //overwrite覆写父类函数，直接覆盖掉原来的方法，用原来的名字，但是方法是新写的【对父类的原方法不改变】
    {
        Console.WriteLine("Child1.F()"); 
    }

    public override void G() //override重写父类虚拟函数,主要实现多态
    {
        Console.WriteLine("Child1.G()");
    }

    public override double H()//override重写父类中抽象方法，这里可以给出具体的函数体
  	{
  		return 1;
   	}
}

class Child2:Parent //子类二继承父类
{
    new public void F()
    {
        Console.WriteLine("Child2.F()");
    }

    public override void G()
    {
        Console.WriteLine("Child2.G()");
    }
}

class Program
{
    static void Main(string[] args)
    {
        Parent child1 = new Child1();
        Parent child2 = new Child2();
        //调用Parent.F()
        child1.F();
        child2.F();
        //实现多态
        child1.G();
        child2.G();
        Parent load = new Parent();
        //重载(overload)
        Console.WriteLine(load.Add(1, 2));
        Console.WriteLine(load.Add(3.4f, 4.5f));
        Console.Read();
    }
}

```

##### 17）抽象类：

###### 关键字 ： abstract

抽象类不能实例化。抽象类的用途是提供对个派生类可以共享的基类的公共定义。例如，类库可以定义一个作为其多个函数的参数的抽象类，并且要求程序员使用该库通过创建派生类来提供自己的类实现。

```
public abstract class A
{
	//类成员
	public abstract void work(int i);//抽象方法
}
```

虚拟方法可以有具体的实现，即有方法体
 抽象方法不能有具体实现，没有方法体，即{},只能子类去实现

抽象类的子类必须实现所有的抽象方法。当抽象类从基类继承到虚拟方法时，可以使用抽象方法重写该虚拟方法。【override】

###### 抽象方法的特性：

- 1）声明用 abstract
- 2）抽象方法是隐式的虚拟方法
- 3）只允许在抽象类中使用抽象方法声明
- 4）一个类可以包括多个抽象方法
- 5）抽象方法没有方法体，没有{}，分号结束
- 6）抽象方法的实现由重写(override)提供，此重写方法时非抽象类的成员
- 7）实现继承用 “ : ”，实现抽象方法用 override
- 8）抽象方法声明不能使用 static 或 virtual
- 9）抽象方法被实现后，不能更改修饰符

###### 抽象属性：

除了声明和调用语法上不一样之外，抽象属性的行为与抽象方法类似，另外抽象属性还有以下特性：

- 1） static 不能与 abstract 连用
- 2）在子类中，通过包括使用 override修饰的属性声明，可以重写抽象类的继承属性
- 3）抽象属性声明不能提供访问器实现，它只能声明该类支持属性，而将访问器实现留给派生子类

```
举例1：抽象类
using System;
using System.Collections.Generic;
using System.Text;

namespace test_2020_2
{
	public abstract class A  //抽象类
	{
		public abstract void DoWork(int i);
	}

    public class D
    {
    	public virtual void DoWork(int i)
    	{
    		//方法体
    	}
    }

    public abstract class E:D //E继承D类
    {
    	public abstract override void DoWork(int i);
    	//因为有 abstract 所以没有具体写
    }

    public class F:E // F继承E
    {
        throw new NotImplementedException();
        //具体实现，这里用抛错代替
    }

}

举例2：抽象类
using System;
using System.Collections.Generic;
using System.Text;

namespace test_2020_2
{
	public abstract class Shape
	{
		private string name;

		public Shape(string s)
		{
			Id = s;
		}

		public string id
		{
			get
			{
				return name;
			}
			set
			{
				name = value;
			}
		}

		public abstract double Area
		{
			get;
		}

		public override string ToString()//存在一个虚拟的ToString()方法
		{
			return Id + "Area = " + string.Format("{0:F2}",Area);
		}
	}


	public class Square:Shape //【正方体】
	{
		private int side;

		public Square(int side,string id) : base(id)
		{
            this.id = id;
		}

        public override double Area
        {
        	get
        	{
        		return side * side;
        	}
        }
	};



	public class Circle:Shape // 圆
	{
		private int radius;//半径		
	    
	    public Circle(int radius,string id) : base(id)
	    {
	    	this.radius = radius;
	    }

	    public override double Area
	    {
	    	get
	    	{
	    		return radius * radius * System.Math.PI;
	    	}
	    } 
	};

    public class Rectangle:Shape // 矩形
    {
    	private int width;
    	private int heigh;

    	public Rectangle(int width,int heigh,string id) : base(id)
    	{
    		this.width = width;
    		this.heigh = heigh;
    	}

    	public override double Area
    	{
    		get
    		{
    			return width * heigh;
    		}
    	}
    }

	class Program
	{
		static viod Main(string[] args)
		{
           Shape[] shapes = 
           {
           	new Shape(5,"Square #1"),
           	new Circle(3,"Circle #1"),
            new Rectangle(4,5,"Rectangle #1")
           };

           Console.WriteLine("Shape Collection");

           foreach (Shape s in shapes)
           {
           	Console.WriteLine(s);        
           }
		}
	}
}
```

##### 18）类的修饰符：

- 1）public ：共有类，所有类都可以访问，不限制对类的访问。
- 2）protected ： 保护类， 表示只能从所在类和所在的类的子类中访问。
- 3）intternal ： 内部类，只有其所在的类才能访问。
- 4）private ： 私有类，只有该类才能访问。
- 5）abstract ： 抽象类，表示一个不完成整的类，不允许建立类的实例。
- 6）sealed ： 封闭类，不允许从该类派生出子类

##### 19）集合类：

- Array类
- Queue类
- Stack类
- HashTable类
- Dictionary类
- 使用集合类导入命名空间：System.Collections

###### ArrayList类:

ArrayList类是一个动态数组类型，其容量会随着需要适当的扩充。
 优点：
 1、支持自动改变大小
 2、可以实现灵活的插入元素
 3、可以灵活的删除元素
 缺点：
 1、更一般的数组比起来速度慢

[],List,ArrayList区别：
 1、[]是针对特定类型，固定长度
 2、List是针对特定类型，任意长度
 3、Array是针对任意类型，固定长度
 4、ArrayList是针对任意类型，任意长度
 5、Array和ArrayList是通过存储Object实现任意类型的，所以需要时间，装箱拆箱

###### Queue类

Queue类：队列，先进先出的数据结构。元素在队尾插入在对头出队。主要是用方法Enqueue(添加元素到尾部),Dequeue(移除并返回Queue开始处的对象),Peek(返回位于Queue开始处的对象，但是不移除)方法。
 优点：
 1、能够对集合进行顺序处理
 2、能够接受null值，允许重复元素

###### stack类

堆栈类，后进先出的数据结构

###### HashTable类

在程序中，存放时数据的常用结构有两种：数组 和 链表
 数组 和 链表 的区别：
 1、数组是将元素在内存中顺序存储的
 2、链表在内存中不是顺序的，而是通过指针逻辑联系到一起
 3、数组必须实现固定好长度，不能适应动态的增减元素的状况
 4、链表可以进行动态的存储分配，可是适应数据的动态增减
 5、静态数组从栈中分配空间，方便快速但是自由度小
 6、链表从堆中分配空间，自由度大但是申请比较麻烦

查询元素的时候 数组 的效率更高，因为数组有下标，但是增减元素很慢
 在进行元素的增减的时候 链表效率很高，但是遍历元素不如数组迅速

HashTbale：既融合了数组的快速查询的优点又兼容了链表的增减元素高效率的特点。

HashTbale类：表示根据键的哈希代码进行组织的 <键-值> 对的集合。用于处理表现类似 key-value  的键值对，其中key通常可以用来快速查找（key区分大小写），value用于存储key的值。HashTbale的key和value都是object类型，可以接收任何类型的键值对

```
举例：
namespace test_2020_2
{

	class Program
	{
		static viod Main(string[] args)
		{
           HashTbale ht = new HashTbale();
           ht.Add(1,"张三");
           ht.Add(2,"李四");
           foreach(DictionaryEntry item in ht)
           {
           	Console.WriteLine("Key = {0},Value = {1}",item.Key,item.Value);
           }
		}
	}
}
```

###### SortLedist类

SortLedist类：
 1、SortedList类表示 键-值 对的集合，这些键和值按键排序并且可以按照索引访问
 2、SortedList最适合对一系列 键-值  对进行排序，在排序的时候，是对键进行排序，其行为类似于HashTbale和Array的混合。当使用item索引器属性按照元素的键访问元素时，其行为类似于HashTbale。当使用GetByindex或SetByindex按照元素的索引访问元素时，其其行为类似于Array。

```
举例：
namespace test_2020_2
{

	class Program
	{
		public static void PrintKeyAndValues(SortedList mylist)
		{
          Console.WriteLine("\t-key-\t-value");
          for (int i = 0 ; i < mylist.Conut;i++)
          {
          	Console.WriteLine("\t:\t" + mylist.GetKey(i) + mylist.GetByIndex(i));
          }
		}


		static viod Main(string[] args)
		{
           SortedList mySL = new SortedList();
           mySL.Add("First","Hello");
           mySL.Add("Second","World");
           mySL.Add("Third","!");

           Console.WriteLine("mySL");
           Console.WriteLine("Conut:" + mySL.Conut);//个数
           Console.WriteLine("capatity:" + mySL.Capatity);//容器容量
		}
	}
}
```

###### Dictionary类

Dictionary类：
 我们使用比较多的非泛型集合类主要有ArrarList类和HashTable类。我们使用HashTable来存储的写入到数据库或者往返信息的时候，需要不断的进行数据类型的转换，增加了拆箱装箱的负担，如果操作的数据类型相对固定的话，可以使用Dictionary<TKey,TValue>集合类来存储就方便很多。例如Dictionary<string,int>。

Dictionary<string,string>是一个泛型它本身有集合的功能。它的特点是存入对象是需要与[Key]值一一对应的存入。

```
举例1：集合类
namespace test_2020_2
{

	class Program
	{
		static viod Main(string[] args)
		{
           Dictionary<int,string> dic = new Dictionary<int,string>();
           dic.Add(1,"Sun");
           dic.Add(4,"Tom");
           dic.Add(3,"Hello");
           dic.Add(2,"world");

           var result = from pair in dic orderby pair.Key select pair;
           //order升序排序
           foreach(KeyValuePair<int,string> pair in result)
           {
           	Console.WriteLine("Key:{0},Value:{1}",pair.Key,pair.Value);
           }

		}
	}
}

举例2：集合类
namespace test_2020_2
{

	class Program
	{
		static viod Main(string[] args)
		{
           Random rnd = new Random();//随机

           string[] maleNames =
           {
           	"Rufus","Bear","Dakota","Fido",
           	"Vanya","Samuel","Koani","Prince"
           };

           string[] famaleNames = 
           {
           	"Maggie","Penny","Saya","Princess",
           	"Abby","Lailla","Sadie","Olivia"
           };

           int mIndex = rnd.Next(maleNames.Length);//随机选中男性名字索引
           int fIndex = rnd.Next(famaleNames.Length);

           Console.WriteLine("For a male:{0}",maleNames[mIndex]);
           Console.WriteLine("For a female:{0}",famaleNames[fIndex]);

		}
	}
}

举例3：集合类-随机类
namespace test_2020_2
{

	class Program
	{
		static viod Main(string[] args)
		{
           byte[] bytest1 = new byte[100];
           byte[] bytest2 = new byte[200];

           Random rnd1 = new Random();
           Random rnd2 = new Random();

           rnd1.NextBytes(bytest1);
           rnd2.NextBytes(bytest2);

           Console.WriteLine("First Series:");

           for (int ctr = bytest1.GetLowerBound(0);ctr <= bytest1.GetUpperBound(0);ctr++)
           {
           	Console.WriteLine("{0,5",bytest1[ctr]);
           	if((ctr + 1)%10 == 0)
           	{
           		Console.WriteLine();
           	}
           }

           Console.WriteLine("Second Series:");

           for (int ctr = bytest1.GetLowerBound(0);ctr < bytest1.GetUpperBound(0);ctr++)
           {
           	Console.WriteLine("{0,5",bytest1[ctr]);
           	if((ctr + 1)%10 == 0)
           	{
           		Console.WriteLine();
           	}
           }

		}
	}
}


举例4：集合类
namespace test_2020_2
{

	class Program
	{
		static viod Main(string[] args)
		{
           char[] delimiterChars = {' ',',','.',':','\t'};//定义分割符号
           string text = "one\ttow three: four,five six seven";

           Console.WriteLine("old text:'{0}'",test);

           string[] words = text.Split(delimiterChars);

           Console.WriteLine("{0} words in text:",words.Length);

           foreach(string s in words)
           {
           	Console.WriteLine(s);
           }

		}
	}
}

举例5：集合类
namespace test_2020_2
{

	class Program
	{
		static viod Main(string[] args)
		{
           string[] separatingChars = {"<<","..."};
           string text = "one<<two......three<four";

           Console.WriteLine("old text:'{0}'",test);

           string[] words = text.Split(separatingChars,StringSplitOptions.RemoveEmptyEntries);

           Console.WriteLine("{0} substring in text:",words.Length);

           foreach(string s in words)
           {
           	Console.WriteLine(s);
           }

		}
	}
}
```

##### 20）字符串String类：

String类的方法：

| 序号 | 方法                                                         | 解释                                                         |
| ---- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 1    | public static int Compare( string strA, string strB )        | 比较两个指定的 string 对象，并返回一个表示它们在排列顺序中相对位置的整数。该方法区分大小写。 |
| 2    | public static int Compare( string strA, string strB, bool ignoreCase ) | 比较两个指定的 string 对象，并返回一个表示它们在排列顺序中相对位置的整数。但是，如果布尔参数为真时，该方法不区分大小写。 |
| 3    | public static string Concat( string str0, string str1 )      | 连接两个 string 对象。                                       |
| 4    | public static string Concat( string str0, string str1, string str2 ) | 连接三个 string 对象。                                       |
| 5    | public static string Concat( string str0, string str1, string str2, string str3 ) | 连接四个 string 对象。                                       |
| 6    | public bool Contains( string value )                         | 返回一个表示指定 string 对象是否出现在字符串中的值。         |
| 7    | public static string Copy( string str )                      | 创建一个与指定字符串具有相同值的新的 String 对象。           |
| 8    | public void CopyTo( int sourceIndex, char[] destination, int destinationIndex, int count ) | 从 string 对象的指定位置开始复制指定数量的字符到 Unicode 字符数组中的指定位置。 |
| 9    | public bool EndsWith( string value )                         | 判断 string 对象的结尾是否匹配指定的字符串。                 |
| 10   | public bool Equals( string value )                           | 判断当前的 string 对象是否与指定的 string 对象具有相同的值。 |
| 11   | public static bool Equals( string a, string b )              | 判断两个指定的 string 对象是否具有相同的值。                 |
| 12   | public static string Format( string format, Object arg0 )    | 把指定字符串中一个或多个格式项替换为指定对象的字符串表示形式。 |
| 13   | public int IndexOf( char value )                             | 返回指定 Unicode 字符在当前字符串中第一次出现的索引，索引从 0 开始。 |
| 14   | public int IndexOf( string value )                           | 返回指定字符串在该实例中第一次出现的索引，索引从 0 开始。    |
| 15   | public int IndexOf( char value, int startIndex )             | 返回指定 Unicode 字符从该字符串中指定字符位置开始搜索第一次出现的索引，索引从 0 开始。 |
| 16   | public int IndexOf( string value, int startIndex )           | 返回指定字符串从该实例中指定字符位置开始搜索第一次出现的索引，索引从 0 开始。 |
| 17   | public int IndexOfAny( char[] anyOf )                        | 返回某一个指定的 Unicode 字符数组中任意字符在该实例中第一次出现的索引，索引从 0 开始。 |
| 18   | public int IndexOfAny( char[] anyOf, int startIndex )        | 返回某一个指定的 Unicode 字符数组中任意字符从该实例中指定字符位置开始搜索第一次出现的索引，索引从 0 开始。 |
| 19   | public string Insert( int startIndex, string value )         | 返回一个新的字符串，其中，指定的字符串被插入在当前 string 对象的指定索引位置。 |
| 20   | public static bool IsNullOrEmpty( string value )             | 指示指定的字符串是否为 null 或者是否为一个空的字符串。       |
| 21   | public static string Join( string separator, string[] value ) | 连接一个字符串数组中的所有元素，使用指定的分隔符分隔每个元素。 |
| 22   | public static string Join( string separator, string[] value, int startIndex, int count ) | 连接接一个字符串数组中的指定位置开始的指定元素，使用指定的分隔符分隔每个元素。 |
| 23   | public int LastIndexOf( char value )                         | 返回指定 Unicode 字符在当前 string 对象中最后一次出现的索引位置，索引从 0 开始。 |
| 24   | public int LastIndexOf( string value )                       | 返回指定字符串在当前 string 对象中最后一次出现的索引位置，索引从 0 开始。 |
| 25   | public string Remove( int startIndex )                       | 移除当前实例中的所有字符，从指定位置开始，一直到最后一个位置为止，并返回字符串。 |
| 26   | public string Remove( int startIndex, int count )            | 从当前字符串的指定位置开始移除指定数量的字符，并返回字符串。 |
| 27   | public string Replace( char oldChar, char newChar )          | 把当前 string 对象中，所有指定的 Unicode 字符替换为另一个指定的 Unicode 字符，并返回新的字符串。 |
| 28   | public string Replace( string oldValue, string newValue )    | 把当前 string 对象中，所有指定的字符串替换为另一个指定的字符串，并返回新的字符串。 |
| 29   | public string[] Split( params char[] separator )             | 返回一个字符串数组，包含当前的 string 对象中的子字符串，子字符串是使用指定的 Unicode 字符数组中的元素进行分隔的。 |
| 30   | public string[] Split( char[] separator, int count )         | 返回一个字符串数组，包含当前的 string 对象中的子字符串，子字符串是使用指定的 Unicode 字符数组中的元素进行分隔的。int 参数指定要返回的子字符串的最大数目。 |
| 31   | public bool StartsWith( string value )                       | 判断字符串实例的开头是否匹配指定的字符串。                   |
| 32   | public char[] ToCharArray()                                  | 返回一个带有当前 string 对象中所有字符的 Unicode 字符数组。  |
| 33   | public char[] ToCharArray( int startIndex, int length )      | 返回一个带有当前 string 对象中所有字符的 Unicode 字符数组，从指定的索引开始，直到指定的长度为止。 |
| 34   | public string ToLower()                                      | 把字符串转换为小写并返回。                                   |
| 35   | public string ToUpper()                                      | 把字符串转换为大写并返回。                                   |
| 36   | public string Trim()                                         | 移除当前 String 对象中的所有前导空白字符和后置空白字符。     |

by 久违 2020.4.9

