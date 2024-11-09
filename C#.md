# C#

# 一、C#入门

## 变量

### decimal

decimal 关键字指示 128 位数据类型。 与浮点型相比，decimal 类型具有更高的精度和更小的范围，这使它适合于财务和货币计算。

### Byte

表示一个 8 位的无符号整数。

### 总结

<img src="D:\akkkkk\study\MyNotes\image\CSharp\\image-20231127193856370" alt="image-20240413233425505" style="zoom:50%;" />

## 常量

前面加const

## 隐式转换

不同类型变量之间的自动转换

- 大范围存小范围。
- 无符号无法隐式存储有符号的
- 有符号的可以隐式存储无符号的，但需看范围

## 显式转换

### 方式

1. 括号强转

   数值之间的转换 低精度 装 高精度

2. Parse法

   把字符串 转成 对应的类型

   ```C#
   i = int.Parse("123");
   ```

3. Convert法

   ```C#
   i = Convert.ToInt32(12.125)
   i = Convert.ToInt32("12.125")
   ```

4. toString法

## 异常捕获

```C#
try
{

}
catch
{

}
```

出错后面不运行，直接跳到catch里。

## 字符串拼接

```c#
Console.WriteLine("hello " + str);

Console.WriteLine("hello {0}", str);
Console.WriteLine("{0} {1}", "hello", str);

string str2 = string.Format("hello {0}", str);
string str3 = string.Format("{0} {1}","hello" , str);
Console.Write(str2);
Console.Write(str3);
```



# 入门练习





# 入门实践











## 控制台知识

```c#
//隐藏光标
Console.CursorVisible = false;

//设置控制台大小
Console.SetWindowSize(50, 20);

//设置缓冲区大小
Console.SetBufferSize(50, 20);

//擦除整个屏幕
Console.Clear();

//改背景颜色，改完一定要clear
Console.BackgroundColor = ConsoleColor.Red;
Console.Clear();

//改变字体颜色
Console.ForegroundColor = ConsoleColor.Yellow;

//隐藏光标
Console.CursorVisible = false;

//设置光标位置（x,y）
Console.SetCursorPosition(x, y);

//在光标处绘制方块。“■”是中文符号，占两个字符
Console.Write("■");

//擦除方块，若要实现可在原位再绘制上空格覆盖即可。
Console.Write("  ");

//得到输入信息，Readkey的参数表示是否显示输入的内容
char c = Console.ReadKey(true).KeyChar;

//控制台的固定参数（注意Console.XXX指的是光标所在位置，实际运用时右侧和下侧都需要记得多-1）
hight = Console.Bufferhight;
width = Console.BufferWidth;


```



## 随机数知识

```c#
Random r = new Random();
a = r.Next(0,10);
```







# 二、C#基础

## 枚举

```c#
enum enumType
{
	A,B,C
}

int temp = int.Parse(Console.ReadLine());
enumType temp2 = (enumType)temp;
```

## 数组

### 一维定义

```c#
int[] arr1;

int[] arr2 = new int[5];

int[] arr3 = new int[5]{1,2,3,4,5};

int[] arr4 = new int[]{1,2,3,4,5,6};

int[] arr5 = {1,2,3,4,5,6};

bool[] arr6 = {true, false};
```

### 二维定义

游戏中一般用来存储 矩阵，在控制台小游戏中可以用二维数组 来表示地图格子

```c#
int[,] arr1;

int[,] arr2 = new int[5,5];

int[,] arr3 = new int[3,3]{ {1,2,3}
                            {4,5,6}
                            {7,8,9} };

int[,] arr4 = new int[,]{ {1,2,3}
                          {4,5,6}
                          {7,8,9} };

int[,] arr5 = { {1,2,3}
                {4,5,6}
                {7,8,9} };
```

### 数组使用

初始化后不能直接增加、删除新的元素，搬家即可。

```c#
Console.WriteLine(arr1.Length);
```

### 拓：交错数组

可以存储同一类型的m行不确定列的数据。

类似matlab的元胞数组。

一般很少使用。

```c#
int[][] arr1;

int[][] arr2 = new int[3][1];

int[][] arr3 = new int[3][]{ new int[] {1,2,3},
                             new int[] {1,2},
                             new int[] {1} };

int[][] arr4 = new int[][]{ new int[] {1,2,3},
                             new int[] {1,2},
                             new int[] {1} };

int[][] arr5 = { new int[] {1,2,3},
                 new int[] {1,2},
                 new int[] {1} };
```

## 值和引用类型

### 引用类型

string，数组，类 

引用类型其实就是多个变量指向同一个内存地址

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20231127210926444.png" alt="image-20231127210926444" style="zoom:50%;" />

### 值类型

除string的其他变量类型、结构体

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20231127210901644.png" alt="image-20231127210901644" style="zoom:50%;" />

### 区别

- 值类型在相互赋值时，把内容拷贝给了对方。它变我不变。

  引用类型的相互赋值，让两者指向同一个值。它变我也变。

- 值类型存储在栈空间，系统分配，自动回收，小而快。

  引用类型存储在堆空间，手动申请和释放，大而慢。

  <img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20231127210704223.png" alt="image-20231127210704223" style="zoom:50%;" />

## String类型

string非常的特殊，它具备值类型的特征 它变我不变。

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20231127211309027.png" alt="image-20231127211309027" style="zoom:50%;" />

string虽然方便，但是有一个小缺点，就是频繁的改变string、重新赋值。会产生内存垃圾。

## 函数

```c#
staic float[] CalcCirc(float r)
{
    return new float[] {3.14f * r *r, 2 * 3.14f *r};
}
```

### ref和out

- 函数参数的修饰符。
- 当传入的值类型参数在内部修改时，或者引用类型参数在内部重新申明时
- 外部的值会发生变化。

ref的使用：传入的参数必须要进行初始化，out不用

out的使用：在内部必须给传入的参数赋值，ref不用

out传入的参数无需初始化，因此在函数内部时一定要给它赋值。

ref传入的参数要初始化，因此在函数内部时不用给他赋值也行。

```c#
class test
{
	static void test22( ref int a)
	{
		//不一定要赋值，因为ref会初始化
        //a=10;
	}
	
	static void test33( out int b)
	{
        //一定要有赋值，因为out不会初始化
        b=10;
	}
	
	static void Main(string[] args)
	{
		int a = 1;
		int b;
    	test22(ref a);
    	test33(out b);
    }
}
```

### 变长参数

变长参数关键字params。

params int[] 意味着可以传入n个int参数，n可以等于0，传入的参数会存在arr数组中。

params关键字后面必为数组，数组的类型可以是任意的类型。

函数参数可以有别的参数，但只能最多出现一个params关键字，并且一定是在最后一组参数。

```c#
class test11
{
     static int Sum(int k, params int[] arr)
     {
         int sum = 0;
         for (int i = 0; i < arr.Length; i++)
         {
             sum += arr[i];
         }
         return sum;
     }
     
    static void Main(string[] args)
    {
        Sum(50);
        Sum(50,1,2,3,4,5,6,7,8,1,22,456,123,1);
    }
}
```



### 默认参数值

有参数默认值的参数 一般称为可选参数。

作用是当调用函数时可以不传入参数，不传就会使用默认值作为参数的值。

支持多参数默认值 每个参数都可以有默认值。

如果要混用 可选参数 必须写在 普通参数后面。

```c#
class test11
{
	static void speak(int k, string test = "aaaaa", string str = "bbbb")
    {
		
    }
    
    static void Main(string[] args)
    {
        speak(10);
    }
}
```



### 重载

```c#
class test11
{
	static void test22(int a)
	{
		return a;
	}
    
    static double test22(double a)
	{
		return a;
	}
}
```



### 递归函数

```c#
// 练习：不允许使用循环语句、条件语句，在控制台中打印出1-280这208个数(提示: 递归+短路)
class test11
{
	static void Fun5(int num)
	{
		Console.WriteLine(num);
		
		// 方法一
		if (num==200) return;
		else return Fun5(num + 1);
		
		// 方法二
		return num==20 || Fun5(num + 1);
	}
}

```



## 结构体

结构体 struct 是**变量和函数**的集合，用来表示特定的数据集合。

public 和private用来修饰变量和方法的。public 外部可以调用，private内部用，不写的话默认就是private。

构造函数没有返回值，函数名和结构体名相同，可以重载。主要是帮助我们快速初始化结构体对象的。

在结构体中申明的变量不能初始化，只能在外部或者在函数中赋值（初始化）。

在结构体中申明的函数 不用加static的。

```c#
class test11
{
    struct Student
    {
        public string name;
        public bool sex;
        public int age;
        public int clas;
        public string major;

        public Student(string name, bool sex, int age, int clas, string major)
        {
            this.name = name;
            this.sex = sex;
            this.age = age;
            this.clas = clas;
            this.major = major;
        }

        public void Speak()
        {
            Console.WriteLine("姓名：{0}性别：{1}年龄：{2}班级：{3}专业：{4}", name, sex ? "女":"男", age, clas, major);
        }
    }
}


```

### 结构体和类的区别

- 结构体是值类型，类是引用类型
- 结构体存在栈中，类存在堆中
- 结构体成员不能使用protected访问修饰符，而类可以
- 结构体成员变量申明不能指定初始值，而类可以
- 结构体不能申明无参的构造函数，而类可以
- 结构体申明有参构造函数后，无参构造不会被顶掉
- 结构体不能申明析构函数，而类可以
- 结构体不能被继承，而类可以
- 结构体需要在构造函数中初始化所有成员变量，而类随意
- 结构体不能被静态static修饰（不存在静态结构体），而类可以



## 排序

### 冒泡排序

两两相邻，不停比较，不停交换，比较m轮

两层循环，外层轮数，内层比较，两值比较，满足交换

优化：比过不比，加入bool

![冒泡排序](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2%E5%86%92%E6%B3%A1%E6%8E%92%E5%BA%8F.gif)



### 选择排序

 新建中间商，依次比较，找出极值，放入目标位置，比较n轮

 两层循环，外层轮数，内层寻找，初始索引，记录极值，内存循环外交换



# C#基础实践



# 三、C#核心

# --封装部分--

## 类与对象



## 构造函数

### 写法

- 没有返回值
- 函数名和类名必须相同
- 没有特殊需求时，一般都是public的
- 构造函数可以被重载
- this代表当前调用该函数的对象自己
- 有参构造会顶掉无参构造

类中是允许自己申明无参构造函数的，结构体是不允许。

自己构造后会失去默认的无参构造，如果不自己实现无参构造函数而实现了有参构造函数

### 特殊写法

可以通过this 重用构造函数代码

访问修饰行[ 构造函数名(参数列表):this(参数1,参数2....)]

对于this(XXX)，XXX可以写常量，也可以写变量，

```c#
class Student
{
    public Person(string name)
    {
        this.name = name;
    }
    
    public Person(int age)
    {
        this.age = age;
    }
    
    public Person(int age, string name):this(name)
    {
        Console.WriteLine("Person两个参数构造函数调用");
    }
}
```





## 析构函数

- 当引用类型的堆内存被回收时，会调用该函数对于需要手动管理内存的语言 (比如C++)，需要在析构函数中做一些内存回收处理
- c#中存在自动垃圾回收机制GC，所以我们几乎不会怎么使用析构函数。除非想在某一个对象被垃圾回收时，做一些特殊处理。
- 析构函数是当垃圾真正被回收的时候，才会调用的函数。
- 在Unity开发中析构函数几乎不会使用。

```c#
~类名()
```



## 垃圾回收机制

### 关于垃圾回收

- 垃圾回收，英文简写GC (Garbage Collector)
- 垃圾回收的过程是在遍历堆(Heap)上动态分配的所有对象
- 通过识别它们是否被引用来确定哪些对象是垃圾，哪些对象仍要被使用
- 所谓的垃圾就是没有被任何变量，对象引用的内容
- 垃圾就需要被回收释放
- 垃圾回收有很多种算法，比如引用计数(Reference Counting)、标记清除(Mark Sweep)、标记整理(Mark Compact)、复制集合(copyCollection)
- GC只负责堆(Heap)内存的垃圾回收
- 引用类型都是存在堆(Heap)中的，所以它的分配和释放都通过垃圾回收机制来管理

### 关于栈

- 浅(stack)上的内存是由系统自动管理的
- 值类型在栈(stack)中分配内存的，他们有自己的申明周期，不用对他们进行管理，会自动分配和释放

### 内存回收机制的大概原理

- C#分为：0代内存	1代内存	2代内存
- 代是垃圾回收机制使用的一种算法 (分代算法)
- 新分配的对象都会被配置在第0代内存中
- 每次分配都可能会进行垃圾回收以释放内存(0代内存满时)
- 大对象（压缩85eee字节 (83kb) 以上的对象为大对象）总被认为是第二代内存，目的是减少性能损耗，提高性能，不会对大对象进行搬迁。

### 内存回收过程

在一次内存回收过程开始时，垃圾回收器会认为堆中全是垃圾，此时会进行的操作：

1. 标记对象。从根(静态字段、方法参数）开始检查引用对象（class……），标记后为可达对象，未标记为不可达对象不可达对象就认为是垃圾
2. 搬迁对象压缩堆 (挂起执行托管代码线程) 释放未标记的对象 搬可达对象 修改引用地址
   **（就是把0代内存的东西搬到1代内存中）**

### 手动进行垃圾回收

系统自动的GC是在检测到某代满了过后才进行，进行一次的时间会比较长，在游戏过程中GC在玩家界面就会出现卡顿的现象。因此一般会在loading的时候进行手动GC。

```c#
//手动触发垃圾回收的方法。
GC.Collect();
```



## 成员属性

成员属性就是普通的一些属性，比如学生类里的name、age、sex等等变量。

为了保护成员属性，防止用户随意更改，可以把成员属性的权限定成private，然后再定义一个属性来讲这个成员属性外包裹一层。

新定义用于包裹的属性可以使用get和set添加一些逻辑语句，在新定义的属性中用逻辑语句，为真正的成员属性赋值。

### get、set的使用注意

- get中需要return内容
- <u>set中用value表示传入的内容</u>
- **get和set语句块中可以加逻辑处理**
- get和set可以加访问修饰符，但是要按照一定的规则进行添加
- get和set可以只有一个（一个一般都是只有get）

### get、set访问修饰符

- 默认不加，会使用属性申明时的访问权限
- 加的访问修饰符要低于属性的访问权限
- 不能让get和set的访问权限都低于属性的权限

### get、set作用

- 成员属性用于<u>保护</u>（可理解为防止用户随意修改）成员变量。就是对属性再裹一层，
- 为成员属性的获取和赋值添加逻辑处理（get）
- 解决3P的局限性（set和get前加3P修饰符，可以让成员变量在外部只能获取、不能修改或者只能修改、不能获取）
  - public：内外访问
  - private：内部访问
  - protected：内部和子类访问

### 自动属性

- 自动属性是属性语句块中只有get和set，一般用于外部能得不能改这种情况
- 如果类中有一个特征是只希望外部能得不能改的，又没什么特殊处理，那么可以直接使用自动属性。

### 示例

```c#
class Student
{
    private string name;
    private int age;
    private int money;
    private bool sex;
    
	//属性的命名一般使用帕斯卡命名法
    public string Name
    {
		get
		{
			//可以在返回之前添加一些逻辑规则
			//意味着这个属性可以获取的内容
			return name;
		}
		
		set
		{
			//可以在设置之前添加一些逻辑规则
			// value关键字,用于表示外部传入的值
			name = value;
		}
    }
    
    public int Money
    {
        get
        {
            //解密处理示例
            return money-5;
        }
        
        set
        {
            //保护处理示例
            if (value<0)
            {
                value=0;
                Console.WriteLine("钱不能少于0.强制设置为0了");
            }
            money=value;
            
            //加密处理示例
            money=value+5;
        }
    }
    
    //自动属性
    public float Height
    {
        //没有在get和set中写逻辑的需求或者想法
        get;
        private set;
    }
}

class test
{
    static void Main(string[] args )
    {
        Console.WriteLine("成员属性");
        Person p = new Person();
        p.Name ="小明";
        Console.WriteLine(p.Name);
        
        p.Money = 1000;
        Console.WriteLine(p.Money);
    }
}
```



## 索引器

结构体里面也是支持索引器

### 作用

让对象可以像数组一样通过索引访问其中元察，使程序看起来更直观更容易编写。

### 固定写法

可以重载

```c#
访问修饰符 返回值 this[参数列表]
{
    get
    {
        
    }
    
    set
    {
        
    }
}
```



```c#
class Person
{
    private string name;
    private int age;
    private Person[] friends;
    
    private int[,] array;
    
    //重载索引器
    public int this[int i,int j]
    {
        get
        {
            return array[i,j];
        }
        set
        {
            array[i,j]=value;
        }
    }
    
    public string this[string str]
    {
        get
        {
            switch(str)
            {
                case "name":
                    return this.name;
                case "age":
                    return age.ToString();
            }
            return "";
        }
    }
    
    public Person this[int index]
    {
		get
        {
            //示例：在索引器中写逻辑，根据需求来处理这里面的内容
            if (friends == null || friends.Length-1<index)
            {
                return null;
            }
            return friends[index];
        }

        set
        {
            //value代表传入的值
		   //可以写逻辑的 根据需求来处理这里面的
            if (friends==null)
            {
                friends=new Person[] {value};
            }
            else if(index>friends.Length-1)
            {
                //自己定了一个规则,如果索引越界就默认把最后一个朋友顶掉
                friends[friends.Length-1]=value;
            }
            friends[index] = value;
        }
    }
}

class test
{
    static void Main(string[] args )
    {
        Console.WriteLine("索引器");
        Person p = new Person();
        p[0]= new Person();
        Console.WriteLine(p[0]);
    }
}

```



## 静态成员

程序中是不能无中生有的我们要使用的对象，变量，函数都是要在内存中分配内存空间的之所以要实例化对象，目的就是分配内存空间，在程序中产生一个抽象的对象

- 静态成员能直接用类名点出使用（全局性）
- 程序开始运行时就会分配内存空间。所以我们就能直接使用。
- 静态成员和程序同生共死。只要使用了它，直到程序结束时内存空间才会被释放
- 一个静态成员就会有自己唯一的一个“内存小房间”这让静态成员就有了唯一性。在任何地方使用都是用的小房间里的内容，改变了它也是改变小房间里的内容。
- 静态成员不会被GC，因此会固定的占用内存，内存过少可能会导致频繁的GC。

### 作用

静态变量常用于唯一变量的申明，方便别人获取的对象申明。

静态方法常用于唯一的方法申明，比如相同规则的数学计算相关函数。

```c#
class test
{
    //静态成员变量
    static public float PI = 3.1415926f;
    //成员变量
    public int testInt = 100;
    
    //静态成员方法，静态函数中不能使用非静态成员
    public static float CalcCircle(float r)
    {
		//成员变量只能将对象实例化出来后才能点出来使用
		//Console.WriteLine(testInt);  //会报错
		Test t = new Test();
		Console.WriteLine(t.testInt);
		return PI * r * r;
    }
    
    //成员方法，非静态函数可以使用静态成员
    public void TestFun()
    {
		Console.writeLine("123");
		Console.WriteLine(PI);
		Console.WriteLine(CalcCircle(2));
    }
}
```

### 常量和静态变量

const (常量)可以理解为特殊的static (静态)。

- 他们都可以通过类名点出使用。
- const必须初始化，不能修改；static没有这个规则。
- const只能修饰变量；static可以修饰很多。
- const一定是写在访问修饰符后面的；static没有这个要求。
- const和static语法放置的位置不一样。

```c#
static public int age1;
public const int age2;
```



## 静态类

用static修饰的类。

- 只能包含静态成员
- 不能被实例化。

### 作用

- 将常用的静态成员写在静态类中，方便使用
- 静态类不能被实例化，更能体现工具类的唯一性。比如 console就是一个静态类



## 静态构造函数

用static修饰的构造函数。

- 静态类和普通类都可以有
- 不能使用访问修饰符
- 不能有参数
- 只会自动调用一次
- 主要在静态构造函数中初始化静态成员



```c#
class test
{
    public static int testInt = 200;
    
    static Test()
    {
    	Console.writeLine("静态构造");
    }
    
    //不算重载
    public Test()
    {
    	Console.WriteLine("普通构造");
    }
    
}
```



## 静态方法

主要是为现有非静态变量类型添加新方法

### 作用

- 提升程序拓展性
- 不需要再对象中重新写方法
- 不需要继承来添加方法
- 为别人封装的类型写额外的

### 特点

- 一定是写在静态类中
- 一定是个静态函数
- 第一个参数为拓展目标第一个参数用this修饰



## 拓展方法

为现有的非静态的变量类型添加方法。

需要将系统自带的非静态类或者自定义的非静态类多加方法时，可以使用拓展方法。

作用

- 提升程序拓展性
- 不需要再在对象中重新写方法
- 不需要继承来添加方法
- 为别人封装的类型写额外的方法

特点

- 静态类中的静态方法
- 第一个参数代表拓展的目标
- 第一个参数前面一定要加 this

注意

- 可以有返回值 和 n个参数
- 根据需求而定





```c#
访问修饰符 static 返回值 函数名(this 拓展类名 参数名，参数类型 参数名,参数类型 参数名...
```



```c#
class test11
{
	public static string speakStringInfo(this string str,ing a,int b)
	{
		Console.WriteLine("为string拓展的方法");
		Console.WriteLine("调用方法对象：" + str);
		Console.WriteLine("添加的参数：" + a + b);
	}
}

class test333
{
    static void Main(string[] args)
    {
        string str = "akkkk";
        str.speakStringInfo(10,20);
    }
}
```





## 运算符重载

让自定义类和结构体能够使用运算符

注意

- 参数的数量
- 条件运算符的配对实现
- 一个符号可以多个重载
- 不能用ref和out

```c#
public static 返回值 operator运算符(参数列表)
```

### 不可重载的运算符

- 逻辑与(&&)
- 逻辑或(ll)
- 索引符 []
- 强转运算符
- 特殊运算符
- 点.
- 三目运算符? :
- 赋值符号=

### 补充

- operator还可以用于类或结构中类型的自定义转换。
- explicit显示转换，implicit隐式转换



## 内部类

默认的内部类是私有的。



## 分布类

把一个类分成几部分申明

关键字：partial

- 用分部描述一个类，可以增加程序的拓展性
- 分部类可以写在多个脚本文件中
- 分部类的访问修饰符要一致
- 分部类中不能有重复成员工



## 分布方法

将方法的申明和实现分离特点

- 不能加访问修饰符 默认私有
- 只能在分部类中申明
- 返回值只能是void
- 可以有参数但不用out关键字



# --继承部分--

## 继承

一个类A继承一个类B，类A将会继承类B的所有成员，A类将拥有B类的所有特征和行为

- 被继承的类称为 父类、基类、超类
- 继承的类称为子类、派生类
- 子类可以有自己的特征和行为
- 单根性：子类只能有一个父类
- 传递性：子类可以间接继承父类的父类
- 极其不建议使用 在子类中申明和父类同名的成员（在多态处理）

```c#
class 类名:被继承的类名
{
	
}
```



## 里氏替换原则

- 里氏替换原则是面向对象七大原则中最重要的原则概念。
- **父类容器装子类对象。**（因为子类对象包含了父类的所有内容）
- 方便进行对象存储和管理

### is

is判断一个对象是否是指是类对象

返回值: bool。是为真，不是为假

```c#
类对象 is 类名
```

### as

将一个对象转换为指定类对象

返回值: 指定类型对象或null。

```c#
类对象 as 类名
```



## 继承的构造函数

父类的父类的构造一>。。。一>父类构造一>。。。一>子类构造

### 父类的无参构造函数

子类实例化时，默认自动调用的是类的无参构造。所以如果父类无参构造被顶掉会报错，子类中就无法默认调用无参构造了，如下：

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20231129192153934.png" alt="image-20231129192153934" style="zoom:50%;" />

### 通过base调用指定父类构造

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20231129192813736.png" alt="image-20231129192813736" style="zoom:50%;" />

this调自己的构造函数，base调父类的构造函数。



## 万物之父

关键字: object

object是所有类型的基类，它是一个类 (引用类型)

- 可以利用里氏替换原则，用object容器装所有对象
- 可以用来表示不确定类型，作为函数参数类型

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20231129193823705.png" alt="image-20231129193823705" style="zoom:50%;" />



## 集装拆箱

- 好处: 不确定类型时可以方便参数的存储和传递，如下：

  <img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20231129194627103.png" alt="image-20231129194627103" style="zoom:50%;" />

- 坏处: 存在内存迁移，增加性能消耗

### 装箱

object是引用类型，object o=a; 表示会在栈上新建一块空间存一块堆的地址。

我们把值类型用引用类型存储，栈内存会迁移到堆内存中的情况称为装箱。

### 装箱

堆内存会迁移到栈内存中，把引用类型存储的值类型取出来则称为装箱。



## 密封类

密封类是让类无法再被继承的类

关键字：sealed

```c#
sealed class Son:Father
```

- 在面向对象程序的设计中，密封类的主要作用就是不允许最底层子类被继承
- 能够加强面向对象程序设计的 规范性、结构性、安全性



# --继承部分--

## 多态

- 多种状态
- 让继承同一父类的子类们，在执行相同方法时有不同的表现 (状态)
- 同一父类的对象执行相同行为 (方法) 有不同的表现
- <u>让同一个对象有唯一行为的特征</u>

### “vob”

- virtual(虚函数)
- override(重写)
- base(父类）

virtual(虚函数)：可以被子类重写。

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20231129200943454.png" alt="image-20231129200943454" style="zoom:50%;" />



## 抽象类

关键字：

- 抽象不能被实例化
- 可以遵循里氏替换原则父类装子类
- 可以实现装载各种毫无关系但是却有相同行为的对象
- 



## 接口

接口是抽象行为的“基类”

接口命名规范：帕斯卡前面加个I

关键字：interface

- 接口值包含 成员方法、属性、索引器、事件，并且都不实现，都没有访问修饰符

- 可以继承多个接口，但是只能继承一个类

- 接口可以继承接口，相当于在进行行为合并，待子类继承时再去实现具体的行为

- 实现的接口方法可以加 virtual关键字，之后子类再重写

  <img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20231129203848643.png" alt="image-20231129203848643" style="zoom:50%;" />

### 显示实现接口

接口被显示实现，主要用于实现不同接口中的同名函数的不同表现

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20231129203257731.png" alt="image-20231129203257731" style="zoom:50%;" />



## 密封方法

用密封关键字sealed 修饰的重写函数，让虚方法或者抽象方法之后不能再被重写。

需要和override一起出现

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20231129204157562.png" alt="image-20231129204157562" style="zoom:50%;" />

# --面向对象相关部分--

## 命名空间

命名空间是用来组织和重用代码的

命名空间就像是一个工具包，类就像是一件一件的工具，都是申明在命名空间中的

关键字：namespace

- 命名空间可以同名分开写，会自动合在一起，像分布类。
- 不同命名空间需要引用。（using XXX; 或 XXX.类）
- 不同命名空间允许有同名类。
- 命名空间可以包裹命名空间。

### 修饰类的访问修饰符

- public 命名空间中的类
- internal 只能在该程序集中使用，默认为internal
- abstract 抽象类
- sealed 密封类
- partial分部类



## 万物之父中的方法

### 静态方法

Equals

- 判断两个对象是否相等

  <img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20231129210918101.png" alt="image-20231129210918101" style="zoom:50%;" />

ReferenceEquals

- 比较两个对象是否是相同的引用，主要是用来比较引用类型的对象

### 成员方法

GetType 

- 该方法在反射相关知识点中是非常重要的方法
- 主要作用就是获取对象运行时的类型Type
- 通过Type结合反射相关知识点可以做很多关于对象的操作

MemberwiseClone

- 修饰类型是protected，用的话需要用clone。
- 该方法用于获取对象的浅拷贝对象（就是会返回一个新的对象，但是新对象中的引用变量会和老对象中一致。）
- （值是深拷贝，引用是浅拷贝）

### 虚方法

Equals

- 默认实现还是比较两者是否为同一个引用，即相当于ReferenceEquals。
- 微软在所有值类型的基类system.ValueType中重写了该方法，用来比较值相等。
- 我们也可以重写该方法，定义自己的比较相等的规则

GetHashCode

- 该方法是获取对象的哈希码(一种通过算法算出的，表示对象的唯一编码，不同对象哈希码有可能一样，具体值根据哈希算法决定)

- 可以通过重写该函数来自己定义对象的哈希码算法，正常情况下使用的极少，基本不用。

  <img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20231129210938751.png" alt="image-20231129210938751" style="zoom:50%;" />

Tostring

- 该方法用于返回当前对象代表的字符串，我们可以重写它定义我们自己的对象转字符串规则

- 非常常用，当我们调用打印方法时，默认使用的就是对象的Tostring方法后打印出来的内容

  <img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20231129210950426.png" alt="image-20231129210950426" style="zoom:50%;" />

## String类

```c#
//字符串本质是char数组
string str = "苏同学";
Console.WriteLine(str[0]);
//打印结果为"苏"

//转为char数组
char[] chars = str.ToCharArray();

//获取字符长度
str.Length

//字符串拼接
str = string.Format("{0}{1}",1,222);

//正向查找字符位置 
str = "我是苏同学？";
int index = str.IndexOf("苏");
//返回 2 字符串的索引 , 找不到就会返回-1

//反向查找字符位置
str = "我是苏同学苏同学？";
index = str.LastIndexOf("苏同学");
//返回 5 从后面开始查找词组就返回第一个字的索引，找不到就返回-1

//移除指定位置后的字符
str = "我是苏同学苏同学";
str = str.Remove(4);
//返回 "我是苏同"

//执行两个参数进行移除 参数1开始的位置 参数2字符个数
str = "我是苏同学陈同学";
str = str.Remove(3,3);
//返回"我是陈同学" 

//替换指定字符串
str = "我是苏同学陈同学";
str = str.Replace("苏同学","李同学");
//返回"我是李同学陈同学" 

//大小写转换
str = "abcdefg";
str = str.ToUpper();
//返回"ABCDEFG"
str = str.ToLower();
//返回"abcdefg"

//字符串截取 截取从指定位置开始之后的字符串
str = "苏同学陈同学";
str = str.Substring(3);
//返回 "陈同学"
//重载 参数1开始位置 参数2指定个数
str = "苏同学陈同学苏同学";
str = str.Substring(3,3);
//返回 "陈同学"

//字符串切割 指定切割符号来切割字符串
str = "1|2|3|4|5|6|7|8";
string[] strs = str.Split("|");
//返回 string[]{1,2,3,4,5,6,7,8}
```



## StringBuilder类

引用命名空间：**System.Text**

关键字：**StringBuilder**

- string是特殊的引用，每次重新赋值或者拼接时会分配新的内存空间。如果一个字符串经常改变会非常浪费空间。
- C#提供用于处理字符串的公共类，能够修改字符串而不创建新的对象，使用它可以提升性能。
- 使用前需要引用命名空间

### 容量

容量和长度（Length）不一样。

容量每次增加时都会自动扩容：

- 申请的时候会预留多一些空间，在增加字符时就可以直接添加。
- 当容量不够时，就分配新的空间，新分配的时候会再扩充容量。

```c#
StringBuilder strBui = new StringBuilder("123123123");
//获得容量
int a = strBui.Capacity;
//默认为16现在已经用了9 自动扩容会x2 变成32 64 128....
```



```c#
StringBuilder strBui = new StringBuilder("123123123");

//增
strBui.Append("444");
//结果为  "123123123444"
strBui.AppendFormat("{0}{1}",555,666);
//结果为  "123123123444555666"

//插入 参数1插入的位置 参数2插入的内容
strBui.Insert(0,"苏同学");
//结果为  "苏同学123123123444555666"

//删  参数1删除开始的位置 参数2删除的个数
strBui.Remove(0,3);
//结果为  "123123123444555666"

//清空
strBui.Clear();
//结果为 ""

//重新赋值 先清空再增加 
strBui.Clear();
strBui.Append("苏同学");

//查 和数组一样
strBui[1];
//结果为 "同"

//改 和数组一样
strBui[0]='李';
//strBui结果为 "李同学"

//替换 参数1被替换的字符  参数2要替换的内容
strBui.Replace("同学","老师");
//strBui结果为 "李老师"

//判断是否相等
strBui.Equals("李老师");
//返回为 true
```



## 结构体和类

### 区别概述

- 结构体和类最大的区别是在存储空间上的，因为结构体是值，类是引用， 一唐老
- 因此他们的存储位置一个在栈上，一个在堆上，
- 通过之前知识点的学习，我相信你能够从此处看出他们在使用的区别一值和引用对象在赋值时的区别。
- 结构体和类在使用上很类似，结构体甚至可以用面向对象的思想来形容一类对象。
- 结构体具备着面向对象思想中封装的持性，但是它不具备继承和多态的特性，因此大大减少了它的使用辆
- 由于结构体不具备继承的特性，所以它不能够使用proted保护访问修饰符。

### 细节区别

- 结构体是值类型，类是引用类型
- 结构体存在栈中，类存在堆中
- 结构体成员不能使用proted访问修饰符，而类可以
- 结构体成员变量申明不能指定初始值，而类可以
- 结构体不能申明无参的构造函数，而类可以
- 结构体申明有参构造函数后，无参构造不会被顶掉
- 结构体不能申明析构函数，而类可以
- 结构体不能被继承，而类可以
- 结构体需要在构造函数中初始化所有成员变量，而类随意
- 结构体不能被静态static修饰（不存在静态结构体）,而类可以
- 结构体不能在自己内部申明和自已一样的结构体变量，而类可以

### 如何选择

- 想要用继承和多态时，直接淘汰结构体，比如玩家，怪物等等
- 对象时数据集合时，优先考虑结构体，比如位置，坐标等等
- 从值类型和引用类型赋值时的区别上去考虑，比如经常被赋值传递的对象，并且
- 改变赋值对象，原对象不想跟着变化时，就用结构体。比如坐标，向量，旋转等等



## 抽象类和接口

### 相同点

- 都可以被继承
- 都不能直接实例化
- 都可以包含方法申明
- 子类必须实现未实现的方法
- 都遵循里氏替换原则

### 区别

- 抽象类中可以有构造函数；接口中不能
- 抽象类只能被单一继承；接口可以被继承多个
  抽象类中可以有成员变量；接口中不能
- 抽象类中可以申明成员方法，虚方法，抽象方法，静态方法；接口中只能申明没有实现的抽象方法
- 抽象类方法可以使用访问修饰符；接口中建议不写

### 如何选择

- 表示对象的用抽象类，表示行为拓展的用接口
- 不同对象拥有的共同行为，我们往往可以使用接口来实现
- 动物是一类对象，我们自然会选择抽象类；而飞翔是一个行为，我们自然会选择接口。

## 面向对象七大原则

开闭原则，依赖倒转原则，里氏替换原则，单一职责原则，接口隔离原则，合成复用原则，迪米特法则。



# C#核心练习

## 类和对象

### 习题一

```c#
GameObject A = new GameObject();
GameObject B = A;
B = null;
A目前等于多少？
```

![image-20231129092321318](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20231129092321318.png)

## 成员变量和访问修饰符

class包裹的东西最终会放在堆中。

引用类型的变量（class等），new一个代表栈和堆都会重新分配一片空间，栈中存放堆的地址。

引用类型的变量（class等），=一个，左侧的变量栈会重新分配一片空间，栈的地址是左侧变量指向的地址。

普通类型的变量（int等），定义赋值，只在栈上分配一片空间，栈中存放变量的值，无堆。

### 习题五

```c#
//Person p = new Person();
//p.age = 10;
//Person p2 = new Person();
//p2.age = 20;
//Console.WriteLine(p.age);
//请问p.age为多少？
```

![image-20231130123836810](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20231130123836810.png)

### 习题六

```c#
Person p = new Person();
p.age = 10;
Person p2 = p;
p2.age = 20;
Console.WriteLine(p.age);
//请问p.age为多少？
```

![image-20231130123955571](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20231130123955571.png)

### 习题七

```c#
#region 练习题七
//Student s = new Student();
//s.age = 10;
//int age = s.age;
//age = 20;
//Console.WriteLine(s.age);
//请问s.age为多少？
#endregion
```

![image-20231130124128111](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20231130124128111.png)

### 习题八

```
#region 练习题八
Student s = new Student();
s.deskmate = new Student();
s.deskmate.age = 10;
Student s2 = s.deskmate;
s2.age = 20;
Console.WriteLine(s.deskmate.age);
//请问s.deskmate.age为多少？
#endregion
```

![image-20231130124353630](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20231130124353630.png)



## 成员方法

### 习题三

```c#
   #region 练习题三
   //定义一个食物类，有名称，热量等特征
   //思考如何和人类以及学生类联系起来
```

人吃食物的角度中，Person中包含使用Food的类的方法即可。

食物被吃的角度中，Food中包含Peoson类的方法即可。



## 构造、析构

### 习题一

```c#
//定义一个学生类，有五种属性，分别为姓名、性别、年龄、CSharp成绩、Unity成绩
//有两个方法：
//一个打招呼：介绍自己交XX，今年几岁了。是男同学还是女同学
//计算自己总分数和平均分并显示的方法
//使用属性完成：年龄必须是0 ~150岁之间，成绩必须是0 ~100
//性别只能是男或女
//实例化两个对象并测试
```



## 索引器

### 习题一

```c#
#region 练习题
//自定义一个整形数组类，该类中有一个整形数组变量
//为它封装增删查改的方法
```



## 万物之父中的方法

### 习题三

```c#
#region 练习题三
//String和string、Int32和int、Int16和short、Int64和long他们的区别是什么？
//string int short long
#endregion
```

前者是后者的别名。

### 习题四

```c#
#region 练习题四
string str = null;
str = "123";
string str2 = str;
str2 = "321";
str2 += "123";
//请问，上面这段代码，分配了多少个新的堆空间
#endregion
```

![image-20231201112359794](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20231201112359794.png)

### 习题五

```c#
//编写一个函数，将输入的字符串反转。不要使用中间商，你必须原地修改输入数组。交换过程中不使用额外空间
//比如：输入{‘h’,‘e’,‘l’,‘l’,‘o’}
//输出      {‘o’,‘l’,‘l’,‘e’,‘h’}
```

![image-20231201113104783](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20231201113104783.png)



# C#核心实践





# 四、C#进阶

## 简单数据结构类

### ArrayList

ArrayList是一个C#为我们封装好的类，本质是一个object类型的数组



### 栈



### 队列





### hash表

![image-20231205091533448](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20231205091533448.png)



## 泛型

- 泛型相当于类型占位符
- 泛型实现了类型参数化，达到代码重用目的。通过类型参数化来实现同一份代码上操作多种类型
- default是默认类型

```c#
class 类名<泛型占位字母>
interface 接口名<泛型占位字母>
函数名<泛型占位字母>(参数列表)
```

### 泛式约束

关键字：where

- 值类型                              where 泛型字母:struct
- 引用类型                            where 泛型字母:class
- 存在无参公共构造函数                 where 泛型字母:new()
- 某个类本身或者其派生类               where 泛型字母:类名
- 某个接口的派生类型                  where 泛型字母:接口名
- 另一个泛型类型本身或者派生类型       where 泛型字母:另一个泛型字母

```c#
class a<T>:where 泛型字母:(约束的类型)
```



## 泛型数据结构

### List 列表

泛型列表

#### **List排序（重要）

- list有自带排序方法sort。
- 自带排序的原因是继承了系统自带的排序接口IComparable。
- 系统自带的变量(int,float,double.....) 一般都可以直接Sort
- 自定义类sort有两种方式，一是继承接口IComparable。二是在Sort中传入委托函数。



### Dictionary 字典

泛型哈希表

### LinkedList 双向链表



### Statck 泛型栈



### Queue 泛型队列



## 委托和事件

### 委托

- 委托是函数(方法)的容器 ，可以理解为表示函数(方法)的变量类型，可以用来存储、传递函数(方法)
- 委托的本质是一个类，用来定义函数(方法)的类型（返回值和参数的类型）
- 不同的函数(方法)必须对应和各自"格式"一致的委托

```C#
访问修饰符 delegate 返回值 委托名(参数列表);
```

#### 系统自带的委托

Action:没有返回值，参数提供了 0~16个委托给我们用

Func:有返回值，参数提供了 0~16个委托给我们用

### 事件

- 事件是基于委托的存在，是委托的安全包裹。
- 事件和委托一样，也是用来存储函数（方法）的。
- 事件只能作为成员存在于类和接口以及结构体中

```c#
访问修饰符 event 委托类型 事件名;
```

### 匿名函数

匿名函数就是没有名字的函数，可以理解为临时的函数变量。

- 匿名函数的使用主要是配合委托和事件进行使用，脱离委托和事件 是不会使用匿名函数的
- 主要是在委托传递和存储时，为了方便可以直接使用该函数
- 但没有办法指定匿名函数移除

```c#
delegate (参数列表)
{
	//函数逻辑
};
```

### Lambad表达式

可以理解为匿名函数的简写

- Lambad除了写法不同外，在使用上和匿名函数一模一样，都是和委托或者事件 配合使用的

```c#
(参数列表)=>{};
```

#### 闭包

（原文链接：https://blog.csdn.net/SerenaHaven/article/details/80047622）

##### 闭包的基本了解

闭包是一个代码块（在C#中，指的是匿名方法或者Lambda表达式，也就是匿名函数），并且这个代码块使用到了代码块以外的变量，于是这个代码块和用到的代码块以外的变量（上下文）被“封闭地包在一起”。当使用此代码块时，该代码块里使用的外部变量的值，是使用该代码块时的值，并不一定是创建该代码块时的值。

（首先）

![image-20240315161542364](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20240315161542364.png)

（其次）

![image-20240315161605650](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20240315161605650.png)

![image-20240315161617699](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20240315161617699.png)

（接着）

![image-20240315161804700](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20240315161804700.png)

![image-20240315162019420](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20240315162019420.png)

![image-20240315162041574](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20240315162041574.png)

![image-20240315162157173](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20240315162157173.png)

- **简单来说，可以理解为，Lambda表达式在传入i的时候，是将i的地址存入的。**
- **for循环只定义了一个i，因此三个匿名函数的参数i均为同一个，而for循环完毕后，i的地址上存储的值为3，因此匿名函数们的参数值都为3.**
- **for循环中定义了3个j，它们分别有不同的地址，值分别为0，1，2。因此，匿名函数们的参数值为0，1，2.**

##### foreach下的闭包

![image-20240315162643681](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20240315162643681.png)

- **简单来说，就是前面for循环中，重复定义了3个j的情况。**

##### 内存泄漏

以下是原文给出的代码：

![image-20240315162839208](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20240315162839208.png)

![image-20240315162902146](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20240315162902146.png)

- **闭包会延长它使用的外部变量的生命周期，直到闭包本身被释放**。
- 

内存泄漏问题，

## 协变和逆变

协变 out；逆变 in。

### 修饰替代符

用来修饰 泛型替代符的  只能修饰接口和委托中的泛型

out修饰的泛型类型，只能作为返回值类型。

in修饰的泛型类型，只能作为参数类型。

### 泛型委托转载

用out和in修饰的泛型委托可以相互装载（有父子关系的泛型）

协变：父类泛型委托装子类泛型委托

逆变：子类泛型委托装父类泛型委托

```c#
//多理解，这里很难，有点看不懂！！！！！！！！！
//协变
fun1<son> os = () =>
{
    return new son();
};

fun1<father> of = os;
father fa = of();


//逆变
fun2<father> iF = (value) =>
{

};

fun2<son> iS = iF;

iS(new son());
```



## 多线程

- 线程类：Thread
- 命名空间：using System.Threading

注意：

- 申明一个新的线程时，线程执行的代码封装到一个函数中。
- 无论是否还有后台线程运行，前台线程结束整个程序就结束了。
- 

```c#
//1.申明一个新的线程 (ThreadMain为线程主函数)
Thread t = new Thread(ThreadMain);

//2.启动线程
t.Start();

//3.设置为后台线程（如果不设置为后台线程 可能导致进程无法正常关闭）
t.IsBackground = true;

//4.关闭释放一个线程（死循环才需特意关闭）
//4.1-死循环中bool标识
Console.ReadKey();
isRuning = false;
Console.ReadKey();

//4.2-通过线程提供的方法(注意在.Net core版本中无法中止 会报错)
try
{
    t.Abort();
    t = null;
}
catch{}
```



## 预处理器指令

```c#
#if
#elif
#else
#endif

#warning
#error
```





## 反射和特性

**（这两个是unity设计的原理基础）**

在程序运行时，通过反射可以得到其它程序集或者自己程序集代码的各种信息：类，函数，变量，对象等等。利用反射可以实例化它们，执行它们，操作它们。

程序正在运行时，可以查看其它程序集或者自身的元数据。

一个运行的程序查看本身或者其它程序的元数据的行为就叫做反射。

### 相关概念

#### 程序集

程序集就是我们写的一个代码集合，我们现在写的所有代码，最终都会被编译器翻译为一个程序集供别人使用，比如一个代码库文件（dll）或者一个可执行文件(exe)

- 程序集是经由编译器编译得到的，供进一步编译执行的那个中间产物
- 在WINDOWS系统中，它一般表现为后缀为·dll（库文件）或者是·exe（可执行文件）的格式

#### 元数据

程序中的类，类中的函数、变量等等信息就是程序的元数据。有关程序以及类型的数据被称为元数据，它们保存在程序集中。

- 元数据就是用来描述数据的数据
- 这个概念不仅仅用于程序上，在别的领域也有元数据



### 反射

#### Type

Type（类的信息类）是反射功能的基础，是访问元数据的主要方式。 

- 使用 Type 的成员获取有关类型声明的信息、有关类型的成员（如构造函数、方法、字段、属性和类的事件）

##### 基础：获取Type

- 万物之父object中的 GetType()可以获取对象的Type
- 通过typeof关键字，传入类名也可以得到对象的Type
- 通过类的名字，也可以获取类型

```c#
int a = 42;

Type type1 = a.GetType();

Type type2 = typeof(int);

Type type3 = Type.GetType("System.Int32");
```

##### 应用：Type使用

事先定义，Type t = typeof(Test)  t为Type类型的变量。Test类是同文件中的，故可以直接typeof。

###### 程序集信息

- 可以通过Type可以得到类型所在程序集信息

```c#
Console.WriteLine(type1.Assembly);
```

###### 构造函数

- ConstructorInfo 是构造函数的反射信息

```c#
//获取所有构造函数
ConstructorInfo[] ctors = t.GetConstructors();
for (int i = 0; i < ctors.Length; i++)
    Console.WriteLine(ctors[i]);

//无参构造
ConstructorInfo info = t.GetConstructor(new Type[0]);
//执行无参构造
Test obj = info.Invoke(null) as Test;

//有参构造
ConstructorInfo info2 = t.GetConstructor(new Type[] { typeof(int) });
//执行有参构造
obj = info2.Invoke(new object[] { 2 }) as Test;

//有参构造
ConstructorInfo info3 = t.GetConstructor(new Type[] { typeof(int), typeof(string) });
//执行有参构造
obj = info3.Invoke(new object[] { 4, "444444" }) as Test;
```

###### 成员

- MemberInfo 是成员的反射信息
- MemberInfo 需要引用命名空间 using System.Reflection

```c#
 //得到所有公共成员
 MemberInfo[] infos = t.GetMembers();
 for (int i = 0; i < infos.Length; i++)
     Console.WriteLine(infos[i]);
```

###### 成员变量

- FieldInfo 是成员变量的反射信息

```c#
//得到所有成员变量
FieldInfo[] fieldInfos = t.GetFields();
for (int i = 0; i < fieldInfos.Length; i++)
    Console.WriteLine(fieldInfos[i]);

//得到指定名称（比如“j”）的公共成员变量
FieldInfo infoJ = t.GetField("j");
Console.WriteLine(infoJ);

//获取对象的某个变量的值
Console.WriteLine(infoJ.GetValue(test));

//设置指定对象的某个变量的值
infoJ.SetValue(test, 100);

//获得infoJ
Type[] infoJTypes = infoJ.GetGenericArguments();

```

###### 成员方法

- MethodInfo 是方法的反射信息
- 静态方法：Invoke中的第一个参数传null即可，因为静态方法直接类名.方法即可

```c#
//得到所有方法
Type strType = typeof(string);
MethodInfo[] methods = strType.GetMethods();

//得到单个方法（存在方法重载用Type数组表示参数类型）
MethodInfo subStr = strType.GetMethod("Substring", new Type[] { typeof(int), typeof(int) });

//得到静态方法


//使用方法（Invoke第一个参数相当于是哪个对象要执行这个成员方法）
object result = subStr.Invoke("Hello,World", new object[] { 7, 5 });

```

###### 枚举

```c#
 //GetEnumName
 //GetEnumNames
```

###### 事件

```c#
 //GetEvent
 //GetEvents
```

###### 接口

```c#
 //GetInterface
 //GetInterfaces
```

###### 属性

```c#
 //GetProperty
 //GetPropertys
```



#### Assembly

程序集类。主要用来加载其它程序集，加载后才能用Type来使用其它程序集中的信息

- 如果想要使用不是自己程序集中的内容 需要先加载程序集。比如 dll文件(库文件) 。
- 可以简单的把库文件看成一种代码仓库，它提供给使用者一些可以直接拿来用的变量、函数或类

##### 加载程序集

- 路径的/需要处理，要么在字符串前加一个@表示取消转义字符/的使用，要么用//替代。

```c#
//同一文件下的其它程序集
Assembly asembly1 = Assembly.Load("程序集名称");

//不在同一文件下的其它程序集
Assembly asembly2 = Assembly.LoadFrom("包含程序集清单的文件的名称或路径");
Assembly asembly3 = Assembly.LoadFile("要加载的文件的完全限定路径");
```



#### Activator

Activator是用于快速实例化对象的类，可以将Type对象快捷实例化为对象。

需要先得到Type，然后快速实例化一个对象。

##### 实例化对象

```c#
Type testType = typeof(Test);
//无参构造
Test testObj = Activator.CreateInstance(testType) as Test;

//有参构造
testObj = Activator.CreateInstance(testType, 99) as Test;
testObj = Activator.CreateInstance(testType, 55, "111222") as Test;
```



### 特性

特性是用于 为元数据再添加更多的额外信息（变量、方法等等）。

- 基本语法：[特性名(参数列表)]
- 可以通过反射获取这些额外的数据来进行一些特殊的处理
- 本质上就是在调用特性类的构造函数
- 一般写在类、函数、变量上一行，表示他们具有该特性信息

#### 自定义特性

- 需要继承特性基类 Attribute

```
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Field, AllowMultiple = true, Inherited = false)]
class MyCustomAttribute : Attribute
{
    //特性中的成员 一般根据需求来写
    public string info;

    public MyCustomAttribute(string info)
    {
        this.info = info;
    }

    public void TestFun()
    {
        Console.WriteLine("特性的方法");
    }
}
```

##### 限制使用范围

通过为特性类 加特性 限制其使用范围

- ```c#
  AttributeUsage(AttributeTargets.Class | AttributeTargets.Struct, AllowMultiple = true, Inherited = true)
  ```

- AttributeTargets —— 特性能够用在哪些地方

- AllowMultiple —— 是否允许多个特性实例用在同一个目标上

- Inherited —— 特性是否能被派生类和重写成员继承

```c#
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Struct, AllowMultiple = true, Inherited = true)]
public class MyCustom2Attribute : Attribute
{

}
```

#### 特性的使用

```c#
[MyCustom("这个是我自己写的一个用于计算的类")]
[MyCustom("这个是我自己写的一个用于计算的类")]
class MyClass
{
    [MyCustom("这是一个成员变量")]
    public int value;

    //[MyCustom("这是一个用于计算加法的函数")]
    //public void TestFun( [MyCustom("函数参数")]int a )
    //{

    //}
    public void TestFun(int a)
    {

    }
}
```

#### 系统自带特性

##### 过时特性

用于提示用户使用的方法等成员已经过时 建议使用新方法

- 关键字：Obsolete，一般加在函数前的特性

- ```c#
  [Obsolete("XXXX", false)]
  ```

- 参数一：调用过时方法时 提示的内容

- 参数二：true-使用该方法时会报错  false-使用该方法时直接警告

```c#
class TestClass
{
    
    [Obsolete("OldSpeak方法已经过时了，请使用Speak方法", false)]
    public void OldSpeak(string str)
    {
         Console.WriteLine(str);
    }

    public void Speak()
    {
		Console.WriteLine(str);
    }
}
```

##### 调用者信息特性

- 需要引用命名空间 System.Runtime.CompilerServices
- 一般作为函数参数的特性

一般分为以下三个：

- CallerFilePath特性：哪个文件调用？
- CallerLineNumber特性：哪一行调用？
- CallerMemberName特性：哪个函数调用？

##### 条件编译特性

- 关键字：Conditional
- 会和预处理指令 #define配合使用
- 需要引用命名空间System.Diagnostics;
- 主要可以用在一些需要调试代码上，比如一些有时想执行有时不想执行的代码

##### 外部dll包函数特性

- 用来标记非.Net(C#)的函数，表明该函数在一个外部的DLL中定义。
- 一般用来调用 C或者C++的Dll包写好的方法
- 需要引用命名空间 System.Runtime.InteropServices



## 迭代器

迭代器是可以让我们在在外部直接通过foreach遍历对象中元素而不需要了解其结构的一种方法。

- 迭代器（iterator）有时又称光标（cursor），是程序设计的软件设计模式。
- 迭代器模式提供一个方法顺序访问一个聚合对象中的各个元素，而又不暴露其内部的标识。
- 迭代器是可以在容器对象（例如链表或数组）上遍历访问的接口，设计人员无需关心容器对象的内存分配的实现细节。
- 可以用foreach遍历的类，都是实现了迭代器的。

### 标准迭代器

- 关键接口：IEnumerator,IEnumerable
- 命名空间：System.Collections
- 可以通过同时继承IEnumerable和IEnumerator，实现其中的方法

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20231208154700227.png" alt="image-20231208154700227" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20231208154720132.png" alt="image-20231208154720132" style="zoom:50%;" />



```c#
class CustomList : IEnumerable, IEnumerator
{
    private int[] list;
    //从-1开始的光标 用于表示 数据得到了哪个位置
    private int position = -1;

    public CustomList()
    {
        list = new int[] { 1, 2, 3, 4, 5, 6, 7, 8 };
    }

    public IEnumerator GetEnumerator()
    {
        Reset();
        return this;
    }

    public object Current
    {
        get
        {
            return list[position];
        }
    }
    
    public bool MoveNext()
    {
        //移动光标
        ++position;
        //是否溢出 溢出就不合法
        return position < list.Length;
    }

    //reset是重置光标位置 一般写在获取 IEnumerator对象这个函数中
    //用于第一次重置光标位置
    public void Reset()
    {
        position = -1;
    }
}
```

### 语法糖实现迭代器

yield return 是C#提供给我们的语法糖

- 语法糖：也称糖衣语法，主要作用就是将复杂逻辑简单化，可以增加程序的可读性，从而减少程序代码出错的机会。
- 关键接口：IEnumerable
- 命名空间：System.Collections
- 让想要通过foreach遍历的自定义类实现接口中的方法GetEnumerator即可

```c#
class CustomList2 : IEnumerable
{
    private int[] list;

    public CustomList2()
    {
        list = new int[] { 1, 2, 3, 4, 5, 6, 7, 8 };
    }

    public IEnumerator GetEnumerator()
    {
        for (int i = 0; i < list.Length; i++)
        {
            //可以理解为暂时返回保留当前的状态，一会还会在回来
            yield return list[i];
        }
        //yield return list[0];
        //yield return list[1];
        //yield return list[2];
        //yield return list[3];
        //yield return list[4];
        //yield return list[5];
        //yield return list[6];
        //yield return list[7];
    }
}
```

### 语法糖为泛型类实现迭代器

```c#
class CustomList<T> : IEnumerable
{
    private T[] array;

    public CustomList(params T[] array)
    {
        this.array = array;
    }

    public IEnumerator GetEnumerator()
    {
        for (int i = 0; i < array.Length; i++)
        {
            yield return array[i];
        }
    }
}
```



## 特殊语法

拓展的一些写法，可以让语法更加优雅。

### var隐式类型

var是一种特殊的变量类型，它可以用来表示任意类型的变量

- var不能作为类的成员，只能用于临时变量申明时。也就是一般写在函数语句块中
- var必须初始化

```c#
var i = 5;
var s = "123";
var array = new int[] { 1, 2, 3, 4 };
var list = new List<int>();
```

### 设置对象初始化

申明对象时，可以通过直接写大括号的形式初始化公共成员变量和属性

```c#
Person p = new Person(100) { sex = true, Age = 18, Name = "唐老狮" };
Person p2 = new Person(200) { Age = 18 };
```

### 设置集合初始化

申明集合对象时，也可以通过大括号直接初始化内部属性

```c#
int[] array2 = new int[] { 1, 2, 3, 4, 5 };

List<int> listInt = new List<int>() { 1, 2, 3, 4, 5, 6 };

List<Person> listPerson = new List<Person>() {
    new Person(200),
    new Person(100){Age = 10},
    new Person(1){sex = true, Name = "唐老狮"}
};

Dictionary<int, string> dic = new Dictionary<int, string>()
{
    { 1, "123" },
    { 2, "222"}
};
```

### 匿名类型

var 变量可以申明为自定义的匿名类型

```c#
var v = new { age = 10, money = 11, name = "小明" };
Console.WriteLine(v.age);
Console.WriteLine(v.name);
```

### 可空类型

- 值类型是不能赋值为空，引用类型可以为空。
- 申明时在值类型后面加? 可以赋值为空。

```c#
//判断是否为空
if( c.HasValue )
{
    Console.WriteLine(c);
    Console.WriteLine(c.Value);
}
    
//安全获取可空类型值
int? value = null;

//如果为空，默认返回值类型的默认值
Console.WriteLine(value.GetValueOrDefault());
//如果为空，也可以指定一个默认值
Console.WriteLine(value.GetValueOrDefault(100));
```



### 空合并操作符

- 空合并操作符 ??
- 左边值 ?? 右边值
- 如果左边值为null就返回右边值，否则返回左边值。
- 只要是可以为null的类型都能用

```c#
int? intV = null;
//int intI = intV == null ? 100 : intV.Value;
int intI = intV ?? 100;
Console.WriteLine(intI);

string str = null;
str = str ?? "hahah";
Console.WriteLine(str);        
```

### 内插字符串

- 关键符号：$
- 用$来构造字符串，让字符串中可以拼接变量

```c#
string name = "唐老狮";
int age = 18;
Console.WriteLine($"好好学习,{name},年龄：{age}");
```



## 值和引用类型

###  值类型和引用类型

F12进到类型的内部去查看，是class就是引用，是struct就是值

### 语句块

- 命名空间
     ↓
  类、接口、结构体
     ↓
  函数、属性、索引器、运算符重载等（类、接口、结构体）
     ↓
  条件分支、循环

- 上层语句块：类、结构体

  中层语句块：函数

  底层的语句块： 条件分支 循环等

- 逻辑代码写在函数、条件分支、循环-中底层语句块中

- 变量申明：

  上、中、底都能申明变量
  上层语句块中：成员变量
  中、底层语句块中：临时变量

### 变量的生命周期

- 编程时大部分都是临时变量，在中底层申明的临时变量（函数、条件分支、循环语句块等）

- 语句块执行结束，没有被记录的对象将被回收或变成垃圾

  值类型：被系统自动回收
  引用类型：栈上用于存地址的房间被系统自动回收，堆中具体内容变成垃圾，待下次GC回收

- 想要不被回收或者不变垃圾，必须将其记录下来（在更高层级记录或者使用静态全局变量记录）

### 结构体中的值和引用

- 结构体本身是值类型

- 前提：该结构体没有做为其它类的成员

  在结构体中的值，栈中存储值具体的内容
  在结构体中的引用，堆中存储引用具体的内容

- 引用类型始终存储在堆中，真正通过结构体使用其中引用类型时只是顺藤摸瓜

### 类中的值和引用

- 类本身是引用类型
- 在类中的值，堆中存储具体的值
- 在类中的引用，堆中存储具体的值
- 值类型跟着大哥走，引用类型一根筋


### 数组中的存储规则

- 数组本身是引用类型
- 值类型数组，堆中房间存具体内容
- 引用类型数组，堆中房间存地址

### 结构体继承接口

- 利用里氏替换原则，用接口容器装载结构体存在装箱拆箱

# C#进阶练习

## hashtable 练习

### 习题二

单例模式

![image-20231205093322662](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_CSharp2image-20231205093322662.png)







# 五、C#知识补充

## Unity跨平台原理

### .Net相关知识

![image-20240520233023129](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618.png)

![image-20240520233109878](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-1.png)

#### .Net 跨语言

![image-20240520233147623](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-2.png)

![image-20240520233220650](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-3.png)

![image-20240520233314785](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-4.png)

##### .Net Framework

![image-20240520233431954](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-5.png)

![image-20240520233536523](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-6.png)

![image-20240520233814417](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-7.png)

- 所有根据CLS规范设计的语言，先转换成CIL代码，然后再通过CLR公共语言进行时，转换成Windows可以使用的机器语言。


![image-20240520234225274](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-8.png)

- **CLR：公共语言运行时。可以看作是个虚拟机。**
- **CIL(IL)：公共中间代码。**

![image-20240520234313664](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-9.png)

![image-20240520234333525](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-10.png)

#### .Net 跨平台

![image-20240520233415326](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-11.png)

##### .Net Core

![image-20240520234540922](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-12.png)

##### Mono

![image-20240520234631321](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-13.png)

![image-20240520234751992](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-14.png)

#### 总结

![image-20240520234954997](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-15.png)

![image-20240520235008307](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-16.png)

![image-20240520235036315](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-17.png)

![image-20240520235138083](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-18.png)

### Unity与Mono

![image-20240520235608388](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-19.png)

![image-20240520235617618](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-20.png)

### Mono

#### 前置知识

![image-20240520235642756](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-21.png)

![image-20240520235743199](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-22.png)

![image-20240520235757881](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-23.png)

#### 跨平台原理

![image-20240521000003472](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-24.png)

![image-20240521000110874](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-25.png)

- unity最开始C#、Java、Boo等都可以使用，但是因为C#太过强大了，其他的语言都渐渐被淘汰了。

![image-20240521000149767](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-26.png)

#### 总结

![image-20240521000249127](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-27.png)

### IL2CPP

![image-20240521000343297](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-28.png)

#### 跨平台原理

![image-20240521000440712](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-29.png)

![image-20240521000543944](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-30.png)

![image-20240521000613972](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-31.png)

#### 总结

![image-20240521001002403](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-32.png)

### 打包问题

#### 类型裁剪

![image-20240521230915469](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-33.png)

#### 泛式问题

![image-20240521231002904](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-34.png)

#### 总结

![image-20240521231359849](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-35.png)

### Mono与IL2CPP

![image-20240521000706320](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-36.png)

![image-20240521000711865](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-37.png)

![image-20240521000805545](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-38.png)

#### 使用建议

![image-20240521000850019](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-39.png)

#### 总结

![image-20240521000926530](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-40.png)

## Unity与C#版本

### 基础知识点

![image-20240521231500398](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-41.png)

![image-20240521231518223](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-42.png)

![image-20240521231536740](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-43.png)

![image-20240521231545096](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-44.png)

![image-20240521231559837](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-45.png)

## C#各版本新功能和语法

![image-20240521232055495](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-46.png)

### C#1-4

![image-20240521232102691](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-47.png)

![image-20240521233122705](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-48.png)

#### 命名和可选参数

好处：可以让我们更方便的调用函数，少写一些重载函数

- 可以在函数调用时，直接用参数名字赋值，不需要根据函数参数的顺序输入。

```c#
Test(1, 1.2f, true);
Test(f: 3.3f, i: 5, b: false);
Test(b: false, f: 3.4f, i: 3);

public void Test(int i, float f, bool b)
{

}

```

- 可以在有默认值参数的函数调用时，不必再重复赋值，只给自己想要的参数赋值即可。

```c#
Test2(1, true, "234");
Test2(1, s: "234");

public void Test2(int i , bool b = true, string s = "123")
{

}
```



#### 动态类型

（不建议使用）

![image-20240521232657888](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-49.png)

动态类型类似于object类型，可以用来存储任意类型。但是在使用动态类型的函数时，不会有提示（因为它可能是任何类型），因此需要自己知道里面有什么函数。

好处：动态类型可以节约代码量，当不确定对象类型，但是确定对象成员时，可以使用动态类型。通过反射处理某些功能时，也可以考虑使用动态类型来替换它

### C#5

![image-20240521233224270](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-50.png)

#### 线程

- Unity支持多线程
- Unity中开启的多线程<u>不能使用主线程中的对象</u>
- Unity中开启多线程后一定记住关闭

```c#
private void Start()
{
    t = new Thread(()=> {
        while (true)
        {
            print("123");
            Thread.Sleep(1000);
        }
    });
    t.Start();
    print("主线程执行");
}

private void OnDestroy()
{
    t.Abort();
}
```

#### 线程池

线程池 是一个C#写好的 装线程的缓存池

优点：可以在我们频繁的需要创建删除线程时提高性能，节约内存

缺点：不能控制线程池中线程的执行顺序，也不能获取线程池内线程取消/异常/完成的通知

![image-20240521233653208](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-51.png)

ThreadPool是一个静态类，里面提供了很多静态成员。

```c#
private void Start()
{
    //1.获取可用的工作线程数和I/O线程数
    int num1;
    int num2;
    ThreadPool.GetAvailableThreads(out num1, out num2);
    print(num1);
    print(num2);


    //3.设置线程池中可以同时处于活动状态的 工作线程的最大数目和I/O线程的最大数目
    //  大于次数的请求将保持排队状态，知直到线程池线程变为可用
    //  更改成功返回true，失败返回false
    if(ThreadPool.SetMaxThreads(20, 20))
    {
        print("更改成功");
    }

    //2.获取线程池中工作线程的最大数目和I/O线程的最大数目
    ThreadPool.GetMaxThreads(out num1, out num2);
    print(num1);
    print(num2);

    //5.设置 工作线程的最小数目和I/O线程的最小数目
    if(ThreadPool.SetMinThreads(5, 5))
    {
        print("设置成功");
    }
    //4.获取线程池中工作线程的最小数目和I/O线程的最小数目
    ThreadPool.GetMinThreads(out num1, out num2);
    print(num1);
    print(num2);

    //6.将方法排入队列以便执行，当线程池中线程变得可用时执行

    ThreadPool.QueueUserWorkItem((obj) =>
    {
        print(obj);
        print("开启了一个线程");
    }, "123452435345");

    for (int i = 0; i < 10; i++)
    {
        ThreadPool.QueueUserWorkItem((obj) =>
        {
            print("第" + obj + "个任务");
        }, i);
    }

    print("主线程执行");
}
```

#### Task任务类

```
//命名空间：System.Threading.Tasks
//类名：Task
```

![image-20240521234900161](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-52.png)

![image-20240522001139877](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-53.png)

##### 创建无返回值Task

```c#
bool isRuning;

private void start()
{
	//1.通过new一个Task对象传入委托函数并启动
    Task t1 = new Task(() =>
    {
        int i = 0;
        while (isRuning)
        {
            print("方式一:" + i);
            ++i;
            Thread.Sleep(1000);
        }
    });
    t1.Start();

    //2.通过Task中的Run静态方法传入委托函数
    Task t2 = Task.Run(() =>
    {
        int i = 0;
        while (isRuning)
        {
            print("方式二:" + i);
            ++i;
            Thread.Sleep(1000);
        }
    });

    //3.通过Task.Factory中的StartNew静态方法传入委托函数
    Task t3 = Task.Factory.StartNew(() =>
    {
        int i = 0;
        while (isRuning)
        {
            print("方式三:" + i);
            ++i;
            Thread.Sleep(1000);
        }
    });
}
```

##### 创建有返回值Task

![image-20240521235706780](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-54.png)

```c#
Task<int> t1;
Task<string> t2;
Task<float> t3;

private void Start()
{
	//1.通过new一个Task对象闯入委托函数并启动
    t1 = new Task<int>(() =>
    {
        int i = 0;
        while (isRuning)
        {
            print("方式一:" + i);
            ++i;
            Thread.Sleep(1000);
        }
        return 1;
    });
    t1.Start();

    //2.通过Task中的Run静态方法传入委托函数
    t2 = Task.Run<string>(() =>
    {
        int i = 0;
        while (isRuning)
        {
            print("方式二:" + i);
            ++i;
            Thread.Sleep(1000);
        }
        return "1231";
    });

    //3.通过Task.Factory中的StartNew静态方法传入委托函数
    t3 = Task.Factory.StartNew<float>(() =>
    {
        int i = 0;
        while (isRuning)
        {
            print("方式三:" + i);
            ++i;
            Thread.Sleep(1000);
        }
        return 4.5f;
    });
}

void Update()
{
    if(Input.GetKeyDown(KeyCode.Space))
    {
        isRuning = false;
        print(t1.Result);
        print(t2.Result);
        print(t3.Result);
    }
}
```

##### 同步执行Task

（了解）

![image-20240521235841130](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132618-55.png)

```
private void Start()
{
	Task t = new Task(() =>
    {
        Thread.Sleep(1000);
        print("哈哈哈");
    });
    //t.Start();
    t.RunSynchronously();
    print("主线程执行");
    //不Start 而是 RunSynchronously，可以同步执行
}
```

##### Task线程阻塞方法

```c#
private void Start()
{
	//1.Wait方法：等待任务执行完毕，再执行后面的内容
    Task t1 = Task.Run(() =>
    {
        for (int i = 0; i < 5; i++)
        {
            print("t1:" + i);
        }
    });

    Task t2 = Task.Run(() =>
    {
        for (int i = 0; i < 20; i++)
        {
            print("t2:" + i);
        }
    });
    t2.Wait();

    //2.WaitAny静态方法：传入任务中任意一个任务结束就继续执行
    Task.WaitAny(t1, t2);

    //3.WaitAll静态方法：任务列表中所有任务执行结束就继续执行
    Task.WaitAll(t1, t2);

    print("主线程执行");
}
```



##### Task完成后继续其它Task

```c#
bool isRuning;
private void Start()
{
	//1.WhenAll静态方法 + ContinueWith方法：传入任务完毕后再执行某任务
    Task.WhenAll(t1, t2).ContinueWith((t) =>
    {
        print("一个新的任务开始了");
        int i = 0;
        while (isRuning)
        {
            print(i);
            ++i;
            Thread.Sleep(1000);
        }
    });

    Task.Factory.ContinueWhenAll(new Task[] { t1, t2 }, (t) =>
    {
        print("一个新的任务开始了");
        int i = 0;
        while (isRuning)
        {
            print(i);
            ++i;
            Thread.Sleep(1000);
        }
    });

    //2.WhenAny静态方法 + ContinueWith方法：传入任务只要有一个执行完毕后再执行某任务
    Task.WhenAny(t1, t2).ContinueWith((t) =>
    {
        print("一个新的任务开始了");
        int i = 0;
        while (isRuning)
        {
            print(i);
            ++i;
            Thread.Sleep(1000);
        }
    });

    Task.Factory.ContinueWhenAny(new Task[] { t1, t2 }, (t) =>
    {
        print("一个新的任务开始了");
        int i = 0;
        while (isRuning)
        {
            print(i);
            ++i;
            Thread.Sleep(1000);
        }
    });
}
```



##### 取消Task执行

```c#
CancellationTokenSource c;
private void Start()
{
	//方法一：通过加入bool标识 控制线程内死循环的结束
	
    //方法二：通过CancellationTokenSource取消标识源类 来控制
    //CancellationTokenSource对象可以达到延迟取消、取消回调等功能

    c = new CancellationTokenSource();
    //延迟取消
    c.CancelAfter(5000);
    //取消回调
    c.Token.Register(() =>
    {
        print("任务取消了");
    });
    Task.Run(() =>
    {
        int i = 0;
        while (!c.IsCancellationRequested)
        {
            print("计时：" + i);
            ++i;
            Thread.Sleep(1000);
        }
    });

    //延迟取消
}

void Update()
{
    if(Input.GetKeyDown(KeyCode.Space))
    {
        c.Cancel();
    }
}
```



#### 异步方法async和await

##### 同步和异步

![image-20240522132600651](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132607.png)

##### 异步编程

![image-20240522132758789](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522132758.png)

##### async和await

![image-20240522133027484](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522133027.png)

![image-20240522133703586](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522133703.png)

##### **举例：复杂逻辑计算**

利用Task新开线程进行计算 计算完毕后再使用 比如复杂的寻路算法

```c#
private void Start()
{
	CalcPathAsync(this.gameObject, Vector3.zero);
}

public async void CalcPathAsync(GameObject obj, Vector3 endPos)
{
    print("开始处理寻路逻辑");
    int value = 10;
    await Task.Run(() =>
    {
        //处理复杂逻辑计算 我这是通过 休眠来模拟 计算的复杂性
        Thread.Sleep(1000);
        value = 50;
        //是多线程 意味着我们不能在 多线程里 去访问 Unity主线程场景中的对象
        //这样写会报错
        //print(obj.transform.position);
    });

    print("寻路计算完毕 处理逻辑" + value);
    obj.transform.position = Vector3.zero;
}
```



##### **举例：计时器**

```c#
CancellationTokenSource source;
private void Start()
{
	Timer();
}

void Update()
{
    if (Input.GetKeyDown(KeyCode.Space))
        source.Cancel();
}

public async void Timer()
{
    UnityWebRequest q = UnityWebRequest.Get("");
    source = new CancellationTokenSource();
    int i = 0;
    while (!source.IsCancellationRequested)
    {
        print(i);
        await Task.Delay(1000);
        ++i;
    }
}
```



##### 举例：资源加载

![image-20240522134224425](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522134224.png)

https://github.com/svermeulen/Unity3dAsyncAwaitUtil



### C#6

 ![image-20240522134702285](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522134702.png)

![image-20240522141249550](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522141249.png)

#### 静态导入

- 用法：在引用命名空间时，在using关键字后面加入static关键词
- 作用：无需指定类型名称即可访问其静态成员和嵌套类型
- 好处：节约代码量，可以写出更简洁的代码

```
using static UnityEngine.Mathf;
using static Test3;

public class Test3
{
    public class Test4
    {

    }

    public static void TTT()
    {
        Debug.Log("123");
    }
}

public class Lesson7 : MonoBehaviour
{
	private void Start()
	{
		//Mathf.Max(10,20);
		Max(10, 20);
		//Test3.Test4 t = new Test3.Test4();
		Test4 t = new Test4();
	}
}

```

#### 异常筛选器

- 用法：在异常捕获语句块中的Catch语句后通过加入when关键词来筛选异常。

  when（表达式）该表达式返回值必须为bool值，如果为ture则执行异常处理，如果为false，则不执行

- 作用：用于筛选异常

- 好处：帮助我们更准确的排查异常，根据异常类型进行对应的处理

```
private void Start()
{
	try
    {
        //用于检查异常的语句块
    }
    catch (System.Exception e) when(e.Message.Contains("301"))
    {
        //当错误编号为301时  作什么处理
        print(e.Message);
    }
    catch (System.Exception e) when (e.Message.Contains("404"))
    {
        //当错误编号为404时  作什么处理
        print(e.Message);
    }
    catch (System.Exception e) when (e.Message.Contains("21"))
    {
        //当错误编号为21时  作什么处理
        print(e.Message);
    }
    catch (System.Exception e)
    {
        //当错误编号为其它时  作什么处理
        print(e.Message);
    }
}
```

#### nameof运算符

- 用法：nameof(变量、类型、成员)通过该表达式，可以将他们的名称转为字符串
- 作用：可以得到变量、类、函数等信息的具体字符串名称

```c#
int i = 10;
//输出：i
print(nameof(i));

//输出：List
print(nameof(List<int>));
//输出：Add
print(nameof(List<int>.Add));

//输出：AI
print(nameof(UnityEngine.AI));

List<int> list = new List<int>() { 1,2,3,4};
//输出：list
print(nameof(list));
//输出：Count
print(nameof(list.Count));
//输出：Add
print(nameof(list.Add));
```



### C#7

![image-20240522135635496](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522135635.png)

![image-20240522135651455](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522135651.png)

![image-20240522141236158](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522141236.png)

![image-20240522144010594](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522144010.png)

#### 字面值改进

- 基本概念：在声明数值变量时，为了方便查看数值，可以在数值之间插入_作为分隔符
- 主要作用：方便数值变量的阅读

```c#
int i = 9_9123_1239;
print(i);
int i2 = 0xAB_CD_17;
print(i2);
```

#### out快捷使用和弃元

- 用法：不需要再使用带有out参数的函数之前，声明对应变量
- 作用：简化代码，提高开发效率

```c#
private void Start()
{
	//1.以前使用带out函数的写法
    //int a;
    //int b;
    //Calc(out a, out b);

    //2.现在的写法
    Calc(out int x, out int y);
    print(x);
    print(y);

    //3.结合var类型更简便(但是这种写法在存在重载时不能正常使用,必须明确调用的是谁)
    Calc(out int a, out var b);
    print(a);
    print(b);

    //4.可以使用 _弃元符号 省略不想使用的参数
    Calc(out int c, out _);
    print(c);
}

public void Calc(out int a, out int b)
{
    a = 10;
    b = 20;
}

public void Calc(out float a, out float b)
{
    a = 10;
    b = 20;
}
```

#### ref修饰临时变量和返回值

- 基本概念：使用ref修饰临时变量和函数返回值，可以让赋值变为引用传递
- 作用：用于修改数据对象中的某些值类型变量

```c#
public struct TestRef
{
    public int atk;
    public int def;

    public TestRef(int atk, int def)
    {
        this.atk = atk;
        this.def = def;
    }
}


class XXX:
private void Start()
{
    //1.修饰值类型临时变量
	//testI2=900,testI=100
	//testI和testI2不是指向栈的同一片空间
	int testI = 100;
    int testI2 = testI;
    testI2 = 900;
    
    //testI2=900,testI=900
    //testI和testI2指向栈的同一片空间
    int testI = 100;
    ref int testI2 = ref testI;
    testI2 = 900;
    
    TestRef r = new TestRef(5,5);
    ref TestRef r2 = ref r;
    r2.atk = 10;
    print(r.atk);

    //2.获取对象中的参数
    ref int atk = ref r.atk;
    atk = 99;
    print(r.atk);

    //3.函数返回值
    //函数和变量都要加ref，才可改变外面的值（类似指针）
    int[] numbers = new int[] { 1, 2, 3, 45, 5, 65, 4532, 12 };
    ref int number = ref FindNumber(numbers, 5);
    number = 98765;
    print(numbers[4]);
}


public ref int FindNumber(int[] numbers, int number)
{
    for (int i = 0; i < numbers.Length; i++)
    {
        if (numbers[i] == number)
            return ref numbers[i];
    }
    return ref numbers[0];
}
```

#### 本地函数

- 基本概念：在函数内部声明一个临时函数
- 注意：
          本地函数只能在声明该函数的函数内部使用
          本地函数可以使用声明自己的函数中的变量
- 作用：方便逻辑的封装
- 建议：把本地函数写在主要逻辑的后面，方便代码的查看

```c#
public int TestTst(int i)
{
    bool b = false;
    i += 10;
    Calc();
    print(b);
    return i;
    
    //本地函数（临时）
    void Calc()
    {
        i += 10;
        b = true;
    }
}
```

#### 抛出表达式

##### throw回顾

- 抛出表达式，就是指抛出一个错误
- 一般的使用方式 都是 throw后面 new 一个异常类
- 异常基类：Exception

```c#
throw new NullReferenceException("1231231");
```

##### C#自带异常类

- IndexOutOfRangeException：当一个数组的下标超出范围时运行时引发。
- NullReferenceException：当一个空对象被引用时运行时引发。
  ArgumentException：方法的参数是非法的
- ArgumentNullException： 一个空参数传递给方法，该方法不能接受该参数
- ArgumentOutOfRangeException： 参数值超出范围
- SystemException：其他用户可处理的异常的基本类
- OutOfMemoryException：内存空间不够
- StackOverflowException 堆栈溢出
- ArithmeticException：出现算术上溢或者下溢
- ArrayTypeMismatchException：试图在数组中存储错误类型的对象
- BadImageFormatException：图形的格式错误
- DivideByZeroException：除零异常
- DllNotFoundException：找不到引用的DLL
- FormatException：参数格式错误
- InvalidCastException：使用无效的类
- InvalidOperationException：方法的调用时间错误
- MethodAccessException：试图访问思友或者受保护的方法
- MissingMemberException：访问一个无效版本的DLL
- NotFiniteNumberException：对象不是一个有效的成员
- NotSupportedException：调用的方法在类中没有实现
- InvalidOperationException：当对方法的调用对对象的当前状态无效时，由某些方法引发。

##### 表达式错误抛出

在C# 7中，可以在更多的表达式中进行错误抛出。好处：更节约代码量

```c#
private void Start()
{
    //1.空合并操作符后用throw
    InitInfo("123");
    //2.三目运算符后面用throw
    GetInfo("1,2,3", 4);
    //3.=>符号后面直接throw
    Action action = () => throw new Exception("错了，不准用这个委托");
    action();
}


private void InitInfo(string str) => jsonStr = str ?? throw new ArgumentNullException(nameof(str));


private string GetInfo(string str, int index)
{
    string[] strs = str.Split(',');
    return strs.Length > index ? strs[index] : throw new IndexOutOfRangeException();
}
```

#### 元组

- 基本概念：多个值的集合，相当于是一种快速构建数据结构类的方式

   一般在函数存在多返回值时可以使用元组 (返回值1类型,返回值2类型,....) 来声明返回值

  在函数内部返回具体内容时通过 (返回值1,返回值2,....)  进行返回

- 主要作用：提升开发效率，更方便的处理多返回值等需要用到多个值时的需求

##### 声明和使用

```c#
public (int, float) yz3;

private void Start()
{
	//1.无变量名元组的声明(获取值：Item'N'作为从左到右依次的参数，N从1开始)
    (int, float,bool,string) yz = (1, 5.5f, true, "123");
    print(yz.Item1);
    print(yz.Item2);
    print(yz.Item3);
    print(yz.Item4);
    //2.有变量名元组的声明
    (int i, float f, bool b, string str) yz2 = (1, 5.5f, true, "123");
    print(yz2.i);
    print(yz2.f);
    print(yz2.b);
    print(yz2.str);

    //3.元组可以进行等于和不等于的判断
    //  数量相同才比较，类型相同才比较，每一个参数的比较是通过==比较 如果都是true 则认为两个元组相等
    if (yz == yz2)
        print("相等");
    else
        print("不相等");

    //元组不仅可以作为临时变量 成员变量也是可以的
    print(this.yz3.Item1);
}
```

##### 函数返回值

```c#
private void Start()
{
	//无变量名函数返回值
    var info = GetInfo();
    print(info.Item1);
    print(info.Item2);
    print(info.Item3);
    //有变量名
    print(info.f);
    print(info.i);
    print(info.str);

    //元组的解构赋值
    //相当于把多返回值元组拆分到不同的变量中
    int myInt;
    string myStr;
    float myFloat;
    (myStr, myInt, myFloat) = GetInfo();
    //(string myStr, int myInt, float myFloat) = GetInfo();
    print(myStr);
    print(myInt);
    print(myFloat);

    //丢弃参数
    //利用传入 下划线_ 达到丢弃该参数不使用的作用
    (string ss, _, _) = GetInfo();
    print(ss);
}

private (string str, int i, float f) GetInfo()
{
    return ("123", 2, 5.5f);
}
```

##### 字典

```c#
private void Start()
{
	//字典中的键 需要用多个变量来控制
    Dictionary<(int i, float f), string> dic = new Dictionary<(int i, float f), string>();
    dic.Add((1, 2.5f), "123");

    if(dic.ContainsKey((1,2.5f)))
    {
        print("存在相同的键");
        print(dic[(1, 2.5f)]);
    }
}
```

#### 模式匹配

- 基本概念：模式匹配时一种语法元素，可以测试一个值是否满足某种条件，并可以从值中提取信息
- 在C#7中，模式匹配增强了两个现有的语言结构：
  1.is表达式，is表达式可以在右侧写一个模式语法，而不仅仅是一个类型
  2.switch语句中的case
- 主要作用：节约代码量，提高编程效率
- **模式匹配用的很多！**

```c#
private void Start()
{
	//1.常量模式(is 常量)：用于判断输入值是否等于某个值
    object o = 1.5f;
    if(o is 1)
    {
        print("o是1");
    }
    if(o is null)
    {
        print("o是null");
    }

    //（用的最多！！）2.类型模式(is 类型 变量名、case 类型 变量名)：用于判断输入值类型，如果类型相同，将输入值提取出来
    //判断某一个变量是否是某一个类型，如果满足会将该变量存入你申明的变量中
    //以前的写法
    //if (o is int)
    //{
    //    int i = (int)o;
    //    print(i);
    //}
    if (o is int i)
    {
        print(i);
    }

    switch (o)
    {
        case int value:
            print("int:" + value);
            break;
        case float value:
            print("float:" + value);
            break;
        case null:
            print("null");
            break;
        default:
            break;
    }


    //3.var模式：用于将输入值放入与输入值相同类型的新变量中
    //相当于是将变量装入一个和自己类型一样的变量中
    if(o is var v)
    {
        print(o);
    }
    //可在判断范围时使用（判断kk是否在[0,10]）
    int kk = GetInt();
    if(kk >= 0 && kk <= 10)
    {

    }

    if (GetInt() is var k && k >= 0 && k <= 10)
    {

    }
}
```



### C#8

![image-20240522144156272](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522144156.png)

![image-20240522144205791](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522144205.png)

#### 静态本地函数

##### 本地函数回顾

- 在C#7的新语法中我们学习了本地函数
- 基本概念：在函数内部声明一个临时函数
- 注意：
          本地函数只能在声明该函数的函数内部使用
          本地函数可以使用声明自己的函数中的变量
- 作用：方便逻辑的封装
- 建议：把本地函数写在主要逻辑的后面，方便代码的查看

```c#
public int CalcInfo(int i)
{
    bool b = false;
    i += 10;
    Calc();
    return i;

    void Calc()
    {
        i += 10;
        b = true;
    }
}

priavte void Start()
{
	print(CalcInfo(10));
}
```

##### C#8新增内容

- 静态本地函数就是在本地函数前方加入静态关键字，让本地函数不能够使用访问封闭范围内（也就是上层方法中）的任何变量
- /作用：让本地函数只能处理逻辑，避免让它通过直接改变上层变量来处理逻辑造成逻辑混乱

```c#
public int CalcInfo(int i)
{
    bool b = false;
    i += 10;
    Calc(ref i, ref b);
    return i;

    static void Calc(ref int i, ref bool b)
    {
        i += 10;
        b = true;
    }
}

priavte void Start()
{
	print(CalcInfo(10));
}
```

#### Using声明

##### 知识回顾

在数据持久化xml相关知识当中，学习了using相关的知识点

![image-20240522144801077](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522144801.png)

```c#
private void Start()
{
	//举例回顾：
    using(StreamWriter strem = new StreamWriter("文件路劲"))
    {
        //对该变量进行逻辑处理 该变量只能在这个语句块中使用
        strem.Write(true);
        strem.Write(1.2f);
        strem.Flush();
        strem.Close();
    }//语句块结束执行时 调用 声明对象的 Dispose方法 释放对象
}
```

##### C#8新增内容

Using 声明就是对using（）语法的简写

当函数执行完毕时 会调用 对象的 Dispose方法 释放对象

```c#
public class TestUsing : IDisposable
{
    public void Dispose()
    {
        
    }
}

class XXX:
private void Start()
{
	using StreamWriter s2 = new StreamWriter("文件路径");
    //对该对象进行逻辑操作
    s2.Write(5);
    s2.Flush();
    s2.Close();
    //利用这个写法 就会在上层语句块执行结束时释放该对象

    //注意：在使用using语法时，声明的对象必须继承System.IDisposable接口
    //因为必须具备Dispose方法，所以当声明没有继承该接口的对象时会报错
    using TestUsing t = new TestUsing();
}
```

#### 空合并赋值

##### 空合并操作符回顾

在C#进阶的特殊语法知识点中学习了 ?? 空合并操作符

- 左边值 ?? 右边值
- 如果左边值为null 就返回右边值 否则返回左边值
- 只要是可以为null的类型都能用

```c#
string str = null;
string str2 = str ?? "234";
print(str2);
//输出：234
```

##### C#8新增内容

- 空合并赋值是C#8.0新加的一个运算符 ??=
- 类似复合运算符
- 左边值 ??= 右边值
- 当左侧为空时才会把右侧值赋值给变量

```c#
string str = null;
str ??= "4565";
print(str);
//输出：4565

//注意：由于左侧为空才会讲右侧赋值给变量，所以不为空的变量不会改变
str ??= "1111";
print(str);
//输出：4565
```



#### 解构函数

##### 元组知识回顾

之前学习过元组的解构，就是可以用单独的变量存储元组的值,相当于把多返回值元组拆分到不同的变量中

```c#
private void Start()
{
	int i;
    float f;
    string s;
    (i,f,_,s) = GetInfo();
}
public (int, float, bool, string) GetInfo()
{
    return (1, 3.4f, true, "123");
}
```

##### C#7的函数内容

- 解构函数Deconstruct （C# 7就有了，讲解时换了顺序）
- 可以在自定义类当中声明解构函数
- 这样可以将该自定义类对象利用元组的写法对其进行变量的获取
- 语法：在类的内部申明函数public void Deconstruct(out 变量类型 变量名, out 变量类型 变量名.....)
- 特点：一个类中可以有多个Deconstruct，但是参数数量不能相同

```c#
public class Person
{
    public string name;
    public bool sex;
    public string number;
    public string email;

    public void Deconstruct(out string n, out bool sex) => (n, sex) = (this.name, this.sex);

    public void Deconstruct(out string n, out bool sex, out string number) => (n, sex, number) = (this.name, this.sex, this.number);

    public void Deconstruct(out string n, out bool sex, out string number, out string email)
    {
        n = name;
        sex = this.sex;
        number = this.number;
        email = this.email;
    }
}


class XXX:
private void Start()
{
	Person p = new Person();
    p.name = "akkkkk";
    p.sex = false;
    p.email = "xxx@163.com";
    p.number = "123123123123";
    
    //可以对该对象利用元组将其具体的变量值解构出来
	//相当于把不同的成员变量拆分到不同的临时变量中
    (string name, bool sex) = p;
    print(name);
    print(sex);
    string str3;
    (_, _, str3) = p;
    print(str3);
}
```

#### 模式匹配

- 模式匹配（Pattern Matching）
- “模式匹配”是一种测试表达式是否具有特定特征的方法
- 在编程里指的是，把一个不知道具体数据信息的内容，通过一些固定的语法格式来确定模式数据的具体内容的过程

##### C#7模式匹配回顾

- 常量模式(is 常量)：用于判断输入值是否等于某个值

- 类型模式(is 类型 变量名、case 类型 变量名)：用于判断输入值类型，如果类型相同，将输入值提取出来

  判断某一个变量是否是某一个类型，如果满足会将该变量存入你申明的变量中

- var模式：用于将输入值放入与输入值相同类型的新变量中

  相当于是将变量装入一个和自己类型一样的变量中

##### C#8增强内容：Switch表达式

- switch表达式是对有返回值的switch语句的缩写

- 用=>表达式符号代替case: 组合

- 用_弃元符号代替default

- 它的使用限制，主要是用于switch语句当中只有一句代码用于返回值时使用

- 语法：

  ```c#
  函数声明 => 变量 switch
  {
      常量 => 返回值表达式,
      常量 => 返回值表达式,
      常量 => 返回值表达式,
      .. ..
      _ => 返回值表达式,
  }
  ```

```c#
public enum PosType
{
    Top_Left,
    Top_Right,
    Bottom_Left,
    Bottom_Right,
}

class XXX:
private void Start()
{
	print(GetPos(PosType.Bottom_Right));
}

public Vector2 GetPos(PosType type) => type switch
{
    PosType.Top_Left => new Vector2(0, 0),
    PosType.Top_Right => new Vector2(1, 0),
    PosType.Bottom_Left => new Vector2(0, 1),
    PosType.Bottom_Right => new Vector2(1, 1),
    _ => new Vector2(0, 0)
};
//原用法：
//{
//    switch (type)
//    {
//        case PosType.Top_Left:
//            return new Vector2(0, 0);
//        case PosType.Top_Right:
//            return new Vector2(1, 0);
//        case PosType.Bottom_Left:
//            return new Vector2(0, 1);
//        case PosType.Bottom_Right:
//            return new Vector2(1, 1);
//        default:
//            return new Vector2(0, 0);
//    }
//}
```

##### C#8增强内容：属性模式

- 就是在常量模式的基础上判断对象上各属性
- 用法：变量 is {属性:值, 属性:值}

```c#
public class DiscountInfo
{
    public string discount;
    public bool isDiscount;

    public DiscountInfo(string discount, bool isDiscount)
    {
        this.discount = discount;
        this.isDiscount = isDiscount;
    }
}

class XXX:
private void Start()
{
	DiscountInfo info = new DiscountInfo("5折", true);
    //if( info.discount == "6折" && info.isDiscount)
    if (info is { discount: "6折", isDiscount: true })
        print("信息相同");

    print(GetMoney(info, 100));

    
}

//结合switch表达式使用,可以通过属性模式判断条件的组合
public float GetMoney(DiscountInfo info, float money) => info switch
{
    //利用属性模式 结合 switch表达式 判断n个条件是否满足
    { discount: "5折", isDiscount: true } => money * .5f,
    { discount: "6折", isDiscount: true } => money * .6f,
    { discount: "7折", isDiscount: true } => money * .7f,
    _ => money
};
```

##### C#8增强内容：元组模式

- 属性模式可以在switch表达式中判断多个变量同时满足再返回什么，但它必须是一个数据结构类对象，判断其中的变量
- 元组模式可以更简单的完成这样的功能，我们不需要声明数据结构类，可以直接利用元组进行判断

```c#
private void Start()
{
	int ii = 10;
    bool bb = true;
    if((ii, bb) is (11, true))
    {
        print("元组的值相同");
    }
    //举例说明
    print(GetMoney("5折", true, 200));
}

public float GetMoney(string discount, bool isDiscount, float money) => (discount, isDiscount) switch
{
    ("5折", true) => money * .5f,
    ("6折", true) => money * .6f,
    ("7折", true) => money * .7f,
    _ => money
};
```

##### C#8增强内容：位置模式

如果自定义类中实现了解构函数，那么可以直接用对应类对象与元组进行is判断

```c#
public class DiscountInfo
{
    public string discount;
    public bool isDiscount;

    public DiscountInfo(string discount, bool isDiscount)
    {
        this.discount = discount;
        this.isDiscount = isDiscount;
    }

    public void Deconstruct(out string dis, out bool isDis)
    {
        dis = this.discount;
        isDis = this.isDiscount;
    }
}

class XXX:
private void Start()
{
    if(info is ("5折", true))
    {
        print("位置模式 满足条件");
    }

    //同样也可以配合switch表达式来处理逻辑
    print(GetMoney2(info, 300));
}

public float GetMoney2(DiscountInfo info, float money) => info switch
{
    ("5折", true) when money > 100 => money * .5f,
    ("6折", true) => money * .6f,
    ("7折", true) => money * .7f,
    _ => money
};

 //补充：可以配合when关键字进行逻辑处理
public float GetMoney3(DiscountInfo info, float money) => info switch
{
    (string dis, bool isDis) when dis == "5折" && isDis => money * .5f,
    (string dis, bool isDis) when dis == "6折" && isDis => money * .6f,
    (string dis, bool isDis) when dis == "7折" && isDis => money * .7f,
    _ => money
};
```

### C#9

待补充。

## 日期和时间

![image-20240522161036199](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522161036.png)

### 时间名词说明

![image-20240522161102553](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522161102.png)

![image-20240522161141501](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/22/20240522161141.png)

### DateTime

- 命名空间：System
- DateTime 是 C# 提供给我们处理日期和时间的结构体
- DateTime 对象的默认值和最小值是0001年1月1日00:00:00（午夜），最大值可以是9999年12月31日晚上11:59:59

#### 初始化

主要参数：

- 年、月、日、时、分、秒、毫秒
- ticks：以格里高利历00:00:00.000年1月1日以来的100纳秒间隔数表示,一般是一个很大的数字

次要参数：

- DateTimeKind：日期时间种类

  ​	Local：本地时间

  ​	Utc：UTC时间

  ​	Unspecified：不指定

- Calendar:日历（使用哪个国家的日历，一般在Unity开发中不使用）

```c#
DateTime dt = new DateTime(2022, 12, 1, 13, 30, 45, 500);
//年、月、日、时、分、秒、毫秒
print(dt.Year + "-" + dt.Month + "-" + dt.Day + "-" + dt.Hour + "-" + dt.Minute + "-" + dt.Second + "-" + dt.Millisecond);

//以格里高利历00:00:00.000年1月1日以来的100纳秒间隔数表示,一般是一个很大的数字
print(dt.Ticks);

//一年的第多少天
print(dt.DayOfYear);

//星期几
print(dt.DayOfWeek);
```

#### 获取时间

```c#
//当前日期和时间
DateTime nowTime = DateTime.Now;
print(nowTime.Minute);
//返回今日日期
DateTime nowTime2 = DateTime.Today;
print(nowTime2.Year + "-" + nowTime2.Month + "-" + nowTime2.Day);
//返回当前UTC日期和时间
DateTime nowTimeUTC = DateTime.UtcNow;
```

#### 计算时间

```c#
//各种加时间
DateTime nowTime3 = nowTime.AddDays(-1);
print(nowTime3.Day);
```

#### 字符串输出

```c#
print(nowTime.ToString());
print(nowTime.ToShortTimeString());
print(nowTime.ToShortDateString());
print(nowTime.ToLongTimeString());
print(nowTime.ToLongDateString());

print(nowTime.ToString("D"));
print(nowTime.ToString("yyyy-MM-dd-ddd/HH-mm-ss"));
```

#### 字符串转DateTime

```c#
//字符串想要转回DateTime成功的话 
//那么这个字符串的格式是有要求的 一定是最基本的 toString的转换出来的字符串才能转回去
//年/月/日 时:分:秒
string str = nowTime.ToString();
str = "1988/5/4 18:00:08";
print(str);
DateTime dt3;
if(DateTime.TryParse(str, out dt3))
{
    print(dt3);
}
else
{
    print("转换失败");
}
```

#### 存储时间

（最常用）

在网络游戏时，可以用来计算玩家间隔的时间（比如隔1天才能抽卡等）

存储时间方式很多：

1. 以直接存字符串
2. 可以直接存Ticks
3. 可以直接存时间戳信息
4. 存储时间戳的形式 更加节约（通过后面的TimeSpan进行计算）

### TimeSpan

- 命名空间：System

- TimeSpan 是 C# 提供给我们的时间跨度结构体

- 用两个DateTime对象相减 可以得到该对象

  ```c#
  TimeSpan ts = DateTime.Now - new DateTime(1970, 1, 1);
  print(ts.TotalMinutes);
  print(ts.TotalSeconds);
  print(ts.TotalDays);
  print(ts.TotalHours);
  print(ts.Ticks);
  
  print(ts.Days + "-" + ts.Hours + "-" + ts.Minutes + "-" + ts.Seconds + "-" + ts.Milliseconds);
  ```

#### 代表时间间隔

```c#
TimeSpan ts2 = new TimeSpan(1,0,0,0);
DateTime timeNow = DateTime.Now + ts2;
```

#### 进行相互计算

```c#
TimeSpan ts3 = new TimeSpan(0, 1, 1, 1);
TimeSpan ts4 = ts2 + ts3;
print(ts4.Days + "-" + ts4.Hours);
```

#### 自带常量

自带的常量方便和ticks进行计算

```c#
print(ts4.Ticks / TimeSpan.TicksPerSecond);
```































