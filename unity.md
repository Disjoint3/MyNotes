# <center>---------Unity知识---------</center>

# unity入门

## 理论知识

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231213174709952.png" alt="image-20231213174709952" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231213174805347.png" alt="image-20231213174805347" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231213174953050.png" alt="image-20231213174953050" style="zoom:50%;" />

### unity模型

一般模型正面都是对着z轴正方向。

一般用空物体作为父对象。

### unity反射机制

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231213180344820.png" alt="image-20231213180344820" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231213180332751.png" alt="image-20231213180332751" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231213180357433.png" alt="image-20231213180357433" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231213180449431.png" alt="image-20231213180449431" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231213180821634.png" alt="image-20231213180821634" style="zoom:50%;" />

### unity游戏场景

游戏场景的本质就是配置文件。



## 脚本基础

### 脚本基本规则

![image-20231213205927890](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231213205927890.png)

### 生命周期函数

![image-20231213185520437](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231213185520437.png)



<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231213190136936.png" alt="image-20231213190136936"  />

- Awake()
- OnEnable()
- Start()
- FixedUpdate()
- Update()
- LateUpdate()
- OnDisable()



```c#
   protected virtual void Awake()
   {
       //在Unity中打印信息的两种方式
       //1. 没有继承MOnoBehavior类的时候
       //Debug.Log("123");
       //Debug.LogError("出错了！！！！！");
       //Debug.LogWarning("警告！！！");
       //2. 继承了MonoBehavior 有一个线程的方法 可以使用
       print("Awake");
   }

   //对于我们来说 想要当一个对象被激活时 进行一些逻辑处理 就可以写在这个函数
   void OnEnable()
   {
       print("OnEnable");
   }

   //主要作用还是用于初始化信息的 但是它相对Awake来说 要晚一点
   //因为它是在对象 进行第一次帧更新之前才会执行的
   void Start()
   {
       print("Start");
   }
   
   //它主要是用于 进行物理更新 
   //它是每一帧的执行的 但是 这里的帧 和游戏帧 有点不同
   //它的时间间隔 是可以在 project setting中的 Time里去设置的
   void FixedUpdate()
   {
       print("FixedUpdate");
   }

   //主要用于处理游戏核心逻辑更新的函数
   void Update()
   {
       print("Update");   
   }

   //一般这个更新是用来处理 摄像机位置更新相关内容的
   //Update和LateUpdate之间 Unity进了一些处理 处理我们动画相关的更新
   void LateUpdate()
   {
       print("LateUpdate");
   }

   //如果我们希望在一个对象失活时做一些处理 就可以在该函数中写逻辑
   void OnDisable()
   {
       print("OnDisable");    
   }

   void OnDestroy()
   {
       print("OnDestroy");    
   }

```



### Inspector窗口可编辑的变量

- Inspector显示的可编辑内容就是脚本的成员变量，私有和保护不额外处理是无法显示编辑的
- Inspector窗口中的变量关联的就是对象的成员变量，运行时改变他们就是在改变成员变量
- 拖曳到GameObject对象后 再改变脚本中变量默认值 界面上不会改变
- 运行中修改的信息不会保存

#### 序列化字段特性

- 序列化就是把一个对象保存到一个文件或数据库字段中去

- 若私有的和保护的变量，可以加上强制序列化字段特性[SerializeField]，让他们被显示

  ```c#
  [SerializeField]
  private int privateInt;
  [SerializeField]
  protected string protectedStr;
  ```

- 若公有的成员变量，可以加上强制序列化字段特性[HideInInspector]，让它不显示在面板上面

  ```c#
  [HideInInspector]
  public int publicInt = 10;
  public bool publicBool = false;
  ```

- 大部分类型都能显示编辑，字典和自定义类不行。

- 字典不能被Inspector窗口显示，没有任何特性可以实现。

- 自定义类型可以加上强制序列化字段特性[System.Serializable]，让它显示在面板上面

#### 其他辅助特性

##### 分组说明特性Header

- 为成员分组

```c#
//[Header("分组说明")]
[Header("基础属性")]
public int age;
public bool sex;
[Header("战斗属性")]
public int atk;
public int def;
```

##### 悬停注释Tooltip

- 为变量添加说明

```c#
//[Tooltip("说明内容")]
[Tooltip("闪避")]
public int miss;
```

##### 间隔特性 Space()

- 让两个字段间出现间隔

```c#
//[Space()]
[Space()]
public int crit;
```

##### 修饰数值的滑条范围Range

- 提供一个滑块来调值，值的范围可以自己设置

```c#
//[Range(最小值, 最大值)]
[Range(0,10)]
public float luck;
```

##### 多行显示字符串Multiline()

- 多行显示字符串
- 默认不写参数显示3行，写参数就是对应行

```c#
//[Multiline(4)]
[Multiline(5)]
public string tips;
```

##### 滚动条显示字符串 TextArea()

- 多行显示字符串，提供滚动条方便查看
- 默认不写参数就是超过3行显示滚动条，最少显示3行，最多4行，超过4行就显示滚动条

```c#
//[TextArea(3, 4)]
[TextArea(3,4)]
public string myLife;
```

##### 变量添加快捷方法 ContextMenuItem()

- 为变量添加快捷方法
- 参数1 显示按钮名
  参数2 方法名，不能有参数

```c#
//[ContextMenuItem("显示按钮名", "方法名")]
[ContextMenuItem("重置钱", "Test")]
public int money;
private void Test()
{
    money = 99;
}
```

##### 方法添加特性ContextMenu()

- 使方法能够在Inspector中执行，主要用来测试。

```c#
//[ContextMenu("测试函数")]
[ContextMenu("哈哈哈哈")]
private void TestFun()
{
    print("测试方法");
}

```



### Mono的重要内容

- MonoBehaviour 类是一个基类，所有 Unity 脚本都默认派生自该类。
- 当从 Unity 的项目窗口创建一个 C# 脚本时，它会自动继承 MonoBehaviour

#### 重要成员

##### 获取依附的GameObject

```c#
print(this.gameObject.name);
```

##### 获取依附的GameObject的位置信息

- 直接transform和gameObject.transform都可以

```c#
print(this.transform.position);//位置
print(this.transform.eulerAngles);//角度
print(this.transform.lossyScale);//缩放大小

print(this.gameObject.transform.position);
```

##### 获取别的脚本对象

```c#
//依附的gameobject和transform位置信息
GameObject otherLesson3;
print(otherLesson3.gameObject.name);
print(otherLesson3.transform.position);
```

##### 获取并设置脚本激活状态

```c#
this.enabled = false;
```

#### 重要方法

- 得到依附对象上挂载的其它脚本

##### 得到自己挂载的单个脚本

- 只要能得到场景中别的对象或者对象依附的脚本，那就可以获取到它的所有信息

```c#
//方法一：根据脚本名获取
//获取脚本的方法 如果获取失败 就是没有对应的脚本 会默认返回空
Lesson3_Test t = this.GetComponent("Lesson3_Test") as Lesson3_Test;
print(t);

//方法二：根据Type获取
t = this.GetComponent(typeof(Lesson3_Test)) as Lesson3_Test;
print(t);

//方法三：根据泛型获取，建议使用泛型获取，因为不用二次转换（常用）
t = this.GetComponent<Lesson3_Test>();
if( t != null )
{
    print(t);
}
```

##### 得到自己挂载的多个脚本

- GetComponents<>()
- GetComponents<>(list)

```c#
//方法一：
Lesson3[] array = this.GetComponents<Lesson3>();

//方法二：
List<Lesson3> list = new List<Lesson3>();
this.GetComponents<Lesson3>(list);
```

##### 得到子对象挂载的脚本

- 它默认也会找自己身上是否挂载该脚本
- 函数是有一个参数的，默认不传是false。（意思就是如果子对象失活，是不会去找这个对象上是否有某个脚本的）
- 函数参数如果传true，及时失活也会找

```c#
//得挂载了单个脚本的子对象
t = this.GetComponentInChildren<Lesson3_Test>(true);

//得挂载了多个脚本的子对象
//方法一：
Lesson3_Test[] lts = this.GetComponentsInChildren<Lesson3_Test>(true);
//方法二：
List<Lesson3_Test> list2 = new List<Lesson3_Test>();
this.GetComponentsInChildren<Lesson3_Test>(true, list2);
```

##### 得到父对象挂载的脚本

它默认也会找自己身上是否挂载该脚本

```c#
//方法一：
t = this.GetComponentInParent<Lesson3_Test>();
print(t);
lts = this.GetComponentsInParent<Lesson3_Test>();
print(lts.Length);

//方法二：list的，省略不写，同前。
```

##### 尝试获取脚本

- 提供了一个更加安全的、获取单个脚本的方法，如果得到了会返回true。然后在来进行逻辑处理即可

```c#
Lesson3_Test l3t;
if(this.TryGetComponent<Lesson3_Test>(out l3t))
{
    //逻辑处理
}
```



## Unity重要组件和API

### GameObject

#### 成员变量

##### 名字

```c#
print(this.gameObject.activeSelf);
```

##### 静态

```c#
print(this.gameObject.isStatic);
```

##### 层级

```c#
print(this.gameObject.layer);
```

##### 标签

```c#
print(this.gameObject.tag);
```

##### transform

```c#
print(this.gameObject.transform.position);
```



#### 静态方法

##### 创建自带几何体

```c#
    //只要得到了一个GameObject对象 我就可以得到它身上挂在的任何脚本信息
    //通过obj.GetComponent来得去
    GameObject obj = GameObject.CreatePrimitive(PrimitiveType.Cube);
    obj.name = "创建的立方体";
```

##### 查找单个对象

- 两种方法：通过对象名查找和通过tag来查找对象
- 无法找到失活的对象，只能找到激活的对象。
- 如果场景中存在多个满足条件的对象，我们无法准确确定找到的是谁 。
- 得到某一个单个对象，可以通过public从外部面板拖，进行关联或者通过API去找。
- GameObject的父类Object提供的方法比较少用。

###### 通过对象名

- 这个查找效率比较低下  因为他会在场景中的所有对象去查找
- 没有找到 就会返回null

```c#
    GameObject obj2 = GameObject.Find("唐老狮");
    if( obj2 != null )
    {
        print(obj2.name);
    }
    else
    {
        print("没有找到对应对象");
    }
```

###### 通过tag

```c#
    //GameObject obj3 = GameObject.FindWithTag("Player");
    //该方法和上面这个方法 效果一样 只是名字不一样而已
    GameObject obj3 = GameObject.FindGameObjectWithTag("Player");
    if (obj3 != null)
    {
        print("根据tag找的对象" + obj3.name);
    }
    else
    {
        print("根据tag没有找到对应对象");
    }
```

##### 查找多个对象

- 找多个对象的API，只能是通过tag去找多个，通过名字是没有找多个的方法的。
- 也是只能找到激活对象，无法找到失活对象。
- GameObject的父类Object提供的方法比较少用。

```c#
GameObject[] objs = GameObject.FindGameObjectsWithTag("Player");
print("找到tag为Player对象的个数" + objs.Length);
```

##### unity Object和万物之父object

- Unity里面的Object不是指的万物之父object
- Unity里的Object 命名空间在UnityEngine中的 Object类 也是集成万物之父的一个自定义类
- C#中的Object 命名空间是在System中的
- 它可以找到场景中挂载的某一个脚本对象。
- 效率更低。前面的GameObject.Find和通过FindWithTag找，只是遍历对象，这个方法不仅要遍历对象 还要遍历对象上挂载的脚本

```c#
Lesson4 o = GameObject.FindObjectOfType<Lesson4>();
print(o.gameObject.name);
```

##### 实例化对象（克隆对象）

- 作用是根据一个GameObject对象，创建出一个和它一模一样的对象。
- 其余操作暂时没有。
- 如果继承了 MonoBehavior，其实可以不用写GameObject，一样可以使用。因为这个方法是Unity里面的Object基类提供给我们的，可以直接用。

```c#
GameObject obj5 = GameObject.Instantiate(myObj);
```

##### 删除对象

###### Destroy

- Destroy有两个参数。第二个参数可写可不写，代表延迟几秒钟删除
- Destroy不仅可以删除对象 还可以删除脚本
- 可以删除指定的一个游戏对象或者删除一个指定的脚本对象。
- Destroy方法不会马上移除对象，只是给这个对象加了一个移除标识 。一般情况下它会在下一帧时，把这个对象移除并从内存中移除。
- 如果是继承MonoBehavior的类 不用写GameObject

```c#
GameObject.Destroy(myObj2);
GameObject.Destroy(obj5, 5);
GameObject.Destroy(this);

//Destroy(myObj2);
```

###### DestroyImmediate

DestroyImmediate可以立即把对象从内存中移除了。

如果没有特殊需求一定要马上移除一个对象的话 ，建议使用上面的 Destroy方法。因为Destroy是异步的，降低卡顿的几率。

```c#
GameObject.DestroyImmediate(myObj);

//DestroyImmediate(myObj);
```

###### 过场景不移除

- 默认情况 在切换场景时 场景中对象都会被自动删除掉
- 如果希望某个对象，过场景不被移除，可以用DontDestroyOnLoad，不想谁过场景被移除就传谁 。

```c#
//自己依附的GameObject对象，过场景不被删除
GameObject.DontDestroyOnLoad(this.gameObject);
    
//如果继承MOnoBehavior也可以直接写
//DontDestroyOnLoad(this.gameObject);
```



#### 成员方法

##### 创建空物体

new一个GameObject就是在创建一个空物体

```c#
    GameObject obj6 = new GameObject();
    GameObject obj7 = new GameObject("创建的空物体");
    GameObject obj8 = new GameObject("顺便加脚本的空物体", typeof(Lesson2),typeof(Lesson1));
```

##### 为对象添加脚本

- 继承MOnoBehavior的脚本不能够去new，如果想要动态的添加继承MonoBehavior的脚本在某一个对象上，直接使用GameObject提供的方法即可。
- 得到脚本的成员方法和继承Mono的类得到脚本的方法 一模一样  

```c#
Lesson1 les1 = obj6.AddComponent(typeof(Lesson1)) as Lesson1;

//用泛型更方便
Lesson2 les2 = obj6.AddComponent<Lesson2>();
```

##### 标签比较

```c#
    if(this.gameObject.CompareTag("Player"))
    {
        print("对象的标签 是 Player");
    }
    if(this.gameObject.tag == "Player")
    {
        print("对象的标签 是 Player");
    }
```

##### 设置激活失活

false 失活，true 激活。

```c#
obj6.SetActive(false);
obj7.SetActive(false);
obj8.SetActive(false);
```

**——————以下次要的成员方法，了解即可。——————**

```c#
    //通知自己 执行什么行为
    //命令自己 去执行这个TestFun这个函数 会在自己身上挂在的所有脚本去找这个名字的函数
    //它会去找到 自己身上所有的脚本 有这个名字的函数去执行
    this.gameObject.SendMessage("TestFun");
    this.gameObject.SendMessage("TestFun2", 199);

    //广播行为 让自己和自己的子对象执行
    //this.gameObject.BroadcastMessage("函数名");

    //向父对象和自己发送消息 并执行
    //this.gameObject.SendMessageUpwards("函数名");
```



### Time

时间相关内容主要用于游戏中参与位移、记时、时间暂停等。

#### 时间缩放比例

- Time.timeScale

```c#
    //时间停止
    Time.timeScale = 0;
    //回复正常
    Time.timeScale = 1;
    //2倍速
    Time.timeScale = 2;
```

#### 帧间隔时间

- Time.deltaTime(帧间隔时间)：最近的一帧用了多长时间（秒）
- 帧间隔时间主要是用来计算位移，路程 = 时间*速度。
- 根据需求 选择参与计算的间隔时间。
- 如果希望游戏暂停时就不动的，那就使用deltaTime。
- 如果希望 不受暂停影响 unscaledDeltaTime。
- 60帧相当于1秒跑60次循环，那么每帧就是16.66ms。

```c#
//受scale影响
print("帧间隔时间" + Time.deltaTime);
    
//不受scale影响的帧间隔时间
print("不受scale影响的帧间隔时间" + Time.unscaledDeltaTime);
```

#### 游戏开始到现在的时间

- Time.frameCount:主要用来计时，单机游戏中计时。

```c#
//受scale影响
print("游戏开始到现在的时间:" + Time.time);

//不受scale影响
print("不受scale影响的游戏开始到现在的时间:" + Time.unscaledTime);
```

#### 物理帧间隔时间 FixedUpdate

```c#
//受scale影响
print(Time.fixedDeltaTime);

//不受scale影响
print(Time.fixedUnscaledDeltaTime);
```

#### 帧数

- 从开始到现在游戏跑了多少帧(次循环)

```c#
print(Time.frameCount);
```



### Transform

#### Vector3

```c#
//常用的一个方法 
//计算两个点之间的距离的方法
print(Vector3.Distance(v1, v12));
```

#### 位置

##### 相对世界坐标系

- 通过position得到的位置，是相对于世界坐标系原点的位置，可能和面板上显示的不一样
- 这是因为如果对象可能有父子关系，且其父对象位置不在原点，那么和面板上肯定就是不一样的

```c#
print(this.gameObject.transform);
print(this.transform.position);
```

##### 相对父对象

- 通过localPosition得到的位置是面板上的位置。

```c#
print(this.transform.localPosition);
```

##### 补充

当父对象的坐标就是世界坐标系原点0,0,0或者对象没有父对象时，他们两个可能出现是一样的情况

位置的赋值不能只改变x，y，z，一改要整体改变

如果只想改一个值，那么有直接赋值或者先取出来、再赋值这两种方法。

```c#
//1.直接赋值
this.transform.position = new Vector3(19, this.transform.position.y, this.transform.position.z);
//2.先取出来 再赋值
//Vector3是可以直接改 xyz的
Vector3 vPos = this.transform.localPosition;
vPos.x = 10;
this.transform.localPosition = vPos;
```

#### 朝向

##### 世界坐标系的朝向

```c#
print(Vector3.zero);//000
print(Vector3.right);//100
print(Vector3.left);//-100
print(Vector3.forward);//001
print(Vector3.back);//00-1
print(Vector3.up);//010
print(Vector3.down);//0-10
```

##### 当前对象的朝向

```c#
//对象当前的面朝向
print(this.transform.forward);
//对象当前的头顶朝向
print(this.transform.up);
//对象当前的右手边
print(this.transform.right);
```

#### 位移

- 明确路程 = 方向 * 速度 * 时间
- 坐标系下的位移计算有两种方式：
  1.自己计算，通过position改变位置
  2.API计算，通过translate移动

##### positon

- 用当前的位置 + 要动的多长距离 = 最终所在的位置
- 决定了前进方向

```c#
this.transform.position = this.transform.position + this.transform.up * 1 * Time.deltaTime;
```

##### translate

- 参数一：表示位移多少  路程 = 方向 * 速度 * 时间
- 参数二：表示 相对坐标系   默认 该参数 是相对于自己坐标系的
- 一般都是用这种方法移动。

###### **V3+World**

```c#
//朝着世界坐标系的Z轴动
this.transform.Translate(Vector3.forward * 1 * Time.deltaTime, Space.World);
```

第一种比较好理解。如图：

![image-20231222143706299](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231222143706299.png)

参考坐标系是世界坐标系（红色的坐标系），V3（0，0，1）相当于往z轴运动。

此时就相当于是**相对于在世界坐标系上往z轴运动，回到自己坐标系上，呈现出的也是世界坐标系的z轴。**运动方向如绿色箭头所示。

###### **this+World**

```c#
//朝着自己的面朝向去动
this.transform.Translate(this.transform.forward * 1 * Time.deltaTime, Space.World);
```

第二种也不难理解， 看图：

![image-20231222144052206](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231222144052206.png)

参考坐标系是世界坐标系，this表示方向是自己坐标系下的面朝向的V3。

此时相当于，是相对于世界坐标系上往物体的面朝向运动。而**世界坐标系上物体的面朝向，回到自己坐标系（蓝色的坐标系）上时，又是和自己坐标系的z轴方向一致**。运动方向如绿色箭头所示。

因此可以看到是始终沿着自己的面移动的。

###### **this+Self**

```c#
//相对于自己的坐标系下的自己的面朝向向量移动 （一定不会这样让物体移动） XXXXXXX
this.transform.Translate(this.transform.forward * 1 * Time.deltaTime, Space.Self);
```

第三种的朝向很奇怪特别讲一下，如图：

![image-20231222145258976](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231222145258976.png)

可以看到，这里是相对于自己坐标系，自己的面朝向运动，刚开始认为，自己坐标系的面朝向应该就是自己坐标系（蓝色的坐标系）的z轴方向才对。

但实际上并非如此。首先参考坐标系是自己的坐标系（蓝色的坐标系），this表示方向是自己坐标系下的面朝向的V3。

**物体的面朝向**（在自己坐标系（蓝色坐标系）**上是其z轴方向，映射到世界坐标系上则是与x轴有一定角度**（设为α）**的方向。而将世界坐标系上的方向呈现在自己坐标系**（蓝色坐标系）**上，则是呈现出z轴向x轴α角度的方向。**因此其方向会如同绿色箭头所示。

###### **V3+Self**

```c#
//朝自己的面朝向移动（相对于自己的坐标系 下的 Z轴正方向移动）
this.transform.Translate(Vector3.forward * 1 * Time.deltaTime, Space.Self);
```

这个比较好理解，如图

![image-20231222145648171](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231222145648171.png)

参考坐标系是自己的坐标系（蓝色），V3相当于是（0，0，1）即z轴方向。合起来就相当于是**沿着物体自己坐标系的z轴方向运动，映射到世界坐标系上如绿色射线所示，而将此射线的方向呈现在自己坐标系上，又是和又是和自己坐标系的z轴方向一致**。运动方向如绿色箭头所示。

因此也能看到是始终沿着自己的面移动的。



#### 角度

- 设置角度和设置位置一样，不能单独设置xyz，要一起设置
- 如果希望改变面板上显示的角度，那就需要改变相对父对象的角度

```c#
//相对世界坐标角度
print(this.transform.eulerAngles);

//相对父对象角度
print(this.transform.localEulerAngles);

//改变面板上的角度
this.transform.localEulerAngles = new Vector3(10, 10, 10);
```



#### 旋转

旋转有两种方法，一是自己计算，二是利用API计算。自己计算部分和位移一样，此处不再赘述。以下均时API计算方法。

##### 自转

- 第一个参数：每一帧转的角度 
- 第二个参数：相对于自己坐标系进行的旋转。默认不填，如果要填可以写相对于世界坐标系进行旋转。

```c#
this.transform.Rotate(new Vector3(0, 10, 0) * Time.deltaTime);
this.transform.Rotate(new Vector3(0, 10, 0) * Time.deltaTime, Space.World);
```

##### 相对于某个轴 

- 和前面的自转差不多。
- 参数一：相对哪个轴进行转动
- 参数二：转动的角度是多少
- 参数三：相对于自己的坐标系进行旋转。默认不填，如果要填可以写相对于世界坐标系进行旋转。
- Y轴转身、X轴抬头低头、Z轴偏头

```c#
this.transform.Rotate(Vector3.right, 10 * Time.deltaTime);
this.transform.Rotate(Vector3.right, 10 * Time.deltaTime, Space.World);
```

##### 相对于某一个点转

- 参数一：相当于哪一个点 转圈圈
- 参数二：相对于点的哪一个轴转圈圈
- 参数三：转的度数  旋转速度 * 时间

```c#
this.transform.RotateAround(Vector3.zero, Vector3.right, 10 * Time.deltaTime);
```



#### 缩放

- 缩放也不能只改xyz，只能一起改
- 并且相对于世界坐标系的缩放大小只能得，不能改
- 一般要修改缩放大小都是改相对于父对象的缩放大小，即localScale
- Unity没有提供关于缩放的API，想要让缩放发生变化，只能自己去写(自己算)

```c#
//相对世界坐标系
print(this.transform.lossyScale);
//相对本地坐标系（父对象）
print(this.transform.localScale);

//改相对于父对象的缩放大小
this.transform.localScale = new Vector3(3, 3, 3);

//慢慢变大
this.transform.localScale += Vector3.one * Time.deltaTime;
```

#### 看向

- 让一个对象的面朝向，看向某一个点或者某一个对象

```c#
//看向一个点，相对于世界坐标系的
this.transform.LookAt(Vector3.zero);
//看向一个对象，传入一个对象的Transform信息
this.transform.LookAt(lookAtObj);
```



### 父子关系

#### 儿子的操作

##### 获取和设置父对象

```c#
//获取父对象
print(this.transform.parent.name);

//设置父对象（断绝父子关系）
this.transform.parent = null;

//设置父对象（认爸爸）
this.transform.parent = GameObject.Find("Father2").transform;
```

###### API实现

- SetParent

- 参数一：我的父亲

- 参数二为只有一个参数的方法的重载，只写参数一那就默认不保留。

- 参数二：是否保留世界坐标的位置、角度、缩放等信息

  true，会保留世界坐标下的状态 ，和父对象进行计算，从而得到本地坐标系信息
  false，不会保留，会把世界坐标系下的位置角度缩放，直接得到本地坐标系

```c#
//断绝父子关系（儿子对父亲）
this.transform.SetParent(null);

//认爸爸
this.transform.SetParent(GameObject.Find("Father2").transform);

//方法重载
this.transform.SetParent(GameObject.Find("Father3").transform, false);
```

##### 其他操作

```c#
//一个对象判断自己是不是另一个对象的儿子
if(son.IsChildOf(this.transform))
{
    print("是我的儿子");
}

//得到自己作为儿子的编号
print(son.GetSiblingIndex());

//把自己设置为第一个儿子
son.SetAsFirstSibling();

//把自己设置为最后一个儿子
son.SetAsLastSibling();

//把自己设置为指定编号的儿子
//编号超出范围不会报错，会直接设置成最后一个编号
son.SetSiblingIndex(1);
```

#### 断绝所有父子关系（父亲对儿子）

- 就是和自己的所有儿子断绝关系，没有父子关系了。
- 注意只能断绝所有一层的儿子关系，孙子还是在儿子的下面。

```c#
this.transform.DetachChildren();
```

#### 获取子对象

- Find方法能够按名字，查找儿子的 transform信息
- 只能找到自己的儿子，找不到自己的孙子
- 能够找到失活的对象，GameObject相关的find查找不能。
- Find方法效率比GameObject.Find相关的要高一些，但是你必须知道父亲是谁才能找

```c#
print(this.transform.Find("Cube (1)").name);
```

##### 遍历得到儿子数量

- childCount得到有多少个儿子，失活的儿子也会算数量，但找不到孙子
- GetChild(i)通过索引号得到自己对应的儿子，i从零开始，编号超出了儿子数量的范围会报错。返回值是对应儿子的transform相关信息。

```c#
for (int i = 0; i < this.transform.childCount; i++)
{
    print("儿子的名字：" + this.transform.GetChild(i).name);
}
```



### 坐标转换

#### 世界坐标转本地坐标

世界坐标系转本地坐标系，可以帮助我们大概判断一个相对位置

##### 点的转换

- InverseTransformPoint()

```c#
//受到缩放影响
print("转换后的点 " + this.transform.InverseTransformPoint(Vector3.forward));
```

##### 方向的转换

- InverseTransformDirection()
- InverseTransformVector()

```c#
//不受缩放影响
print("转换后的方向" + this.transform.InverseTransformDirection(Vector3.forward));
//受缩放影响
print("转换后的方向(受缩放影响)" + this.transform.InverseTransformVector(Vector3.forward));
```

#### 本地坐标转世界坐标

##### 点的转换

- TransformPoint()
- 本地坐标系的点转世界坐标系的点最重要
- 比如，现在玩家要在自己面前的n个单位前放一团火。这个时候不用关心世界坐标系，通过相对于本地坐标系的位置转换为世界坐标系的点，进行特效的创建或者攻击范围的判断。

```c#
//受到缩放影响
print("本地转世界点" + this.transform.TransformPoint(Vector3.forward));
```

##### 方向的转换

- TransformDirection()
- TransformVector()

```c#
//不受缩放影响
print("本地转世界方向" + this.transform.TransformDirection(Vector3.forward));
//受缩放影响
print("本地转世界方向" + this.transform.TransformVector(Vector3.forward));
```



### Input（输入相关）

- 输入相关内容肯定是写在Update中的。
- 同样的Input中提供了许多的API供用户使用。

#### 鼠标在屏幕位置

- 屏幕坐标的原点是在屏幕的左下角，往右是X轴正方向，往上时Y轴正方向。
- 返回值时Vector3，但只有x和y有值，z一直是0。这是因为屏幕本来就是2D的，不存在Z轴。

```c#
print(Input.mousePosition);
```

#### 检测鼠标输入

```c#
//鼠标按下一瞬间会进入
//0左键、1右键、2中键
//只要按下的这一瞬间会进入一次
if( Input.GetMouseButtonDown(0) )
{
    print("鼠标左键按下了");
}
       
//鼠标抬起一瞬间进入
if( Input.GetMouseButtonUp(0) )
{
    print("鼠标左键抬起了");
}

//鼠标长按按下抬起都会进入
//当按住按键不放时，会一直进入这个判断
if( Input.GetMouseButton(1))
{
    print("右键按下");
}

//中键滚动
//返回值为y，-1往下滚、0没有滚、1往上滚
//返回值是Vector的值，鼠标中键滚动会改变其中的Y值
print(Input.mouseScrollDelta);
```

#### 检测键盘输入

```c#
//键盘按下
if( Input.GetKeyDown(KeyCode.W) )
{
    print("W键按下");
}

//传入字符串的重载
//这里传入的 字符串 不能是大写的 不然会报错
//只能传入小写字符串
if( Input.GetKeyDown("q") )
{
    print("q按下");
}
       
//键盘抬起
if( Input.GetKeyUp(KeyCode.W) )
{
    print("W键抬起");
}

//键盘长按
if( Input.GetKey(KeyCode.W) )
{
    print("W键长按");
}
```

####  检测默认轴输入

- Unity提供了更方便的方法，来帮助我们控制对象的位移和旋转。
- 默认的GetAxis方法是有渐变的，会总在-1~0~1之间渐变，会出现小数
- GetAxisRaw方法 和 GetAxis使用方式相同，只不过其返回值只会是 -1 0 1 不会有中间值

```c#
 //键盘AD按下时，返回-1到1之间的变换
 //得到的这个值就是左右方向，可以通过它来控制对象左右移动或旋转
 float h = Input.GetAxis("Horizontal");
 print(h);

 //键盘SW按下时，返回-1到1之间的变换
 //得到的这个值就是上下方向，可以通过它来控制对象上下移动或旋转
 print(Input.GetAxis("Vertical"));

 //鼠标横向移动时，返回-1到1左右的变换
 print(Input.GetAxis("Mouse X"));

 //鼠标竖向移动时，返回-1到1下上的变换
 print(Input.GetAxis("Mouse Y"));
```

#### 其它

##### 触屏

```c#
//是否有任意键或鼠标长按
if(Input.anyKey)
{
    print("有一个键长按");
}

//是否有任意键或鼠标按下
if(Input.anyKeyDown)
{
    print("有一个键 按下");
    //这一帧的键盘输入
    print(Input.inputString);
}
```

##### 手柄

```c#
//手柄输入相关
//得到连接的手柄的所有按钮名字
string[] strs = Input.GetJoystickNames();

//某一个手柄键按下
if( Input.GetButtonDown("Jump") )
{

}

//某一个手柄键抬起
if (Input.GetButtonUp("Jump"))
{

}

//某一个手柄键长按
if (Input.GetButton("Jump"))
{

}
```

##### 移动设备

```c#
//移动设备触摸相关
if(Input.touchCount > 0)
{
    Touch t1 = Input.touches[0];
    //位置
    print(t1.position);
    //相对上次位置的变化
    print(t1.deltaPosition);
}

//是否启用多点触控
Input.multiTouchEnabled = false;
```

##### 陀螺仪

```c#
//陀螺仪（重力感应）
//是否开启陀螺仪 必须开启 才能正常使用
Input.gyro.enabled = true;
//重力加速度向量
print(Input.gyro.gravity);
//旋转速度
print(Input.gyro.rotationRate);
//陀螺仪 当前的旋转四元数 
//比如 用这个角度信息 来控制 场景上的一个3D物体受到重力影响
//手机怎么动 它怎么动
print(Input.gyro.attitude);
```



### Screen（屏幕相关）

#### 静态属性

##### 常用

```c#
//当前屏幕（显示器的）分辨率
Resolution r = Screen.currentResolution;
print("当前屏幕分辨率的宽" + r.width + "高" + r.height);

//屏幕窗口当前宽高
//这得到的是当前窗口的宽高，不是设备分辨率的宽高
//一般写代码要用窗口宽高，做计算时就用他们
print(Screen.width);
print(Screen.height);

//屏幕休眠模式 
Screen.sleepTimeout = SleepTimeout.NeverSleep;
```

##### 不常用

```c#
//运行时是否全屏模式
Screen.fullScreen = true;

//窗口模式：
//独占全屏FullScreenMode.ExclusiveFullScreen
//全屏窗口FullScreenMode.FullScreenWindow
//最大化窗口FullScreenMode.MaximizedWindow
//窗口模式FullScreenMode.Windowed
Screen.fullScreenMode = FullScreenMode.Windowed;

//移动设备屏幕转向相关
//允许自动旋转为左横向 Home键在左
Screen.autorotateToLandscapeLeft = true;
//允许自动旋转为右横向 Home键在右
Screen.autorotateToLandscapeRight = true;
//允许自动旋转到纵向 Home键在下
Screen.autorotateToPortrait = true;
//允许自动旋转到纵向倒着看 Home键在上
Screen.autorotateToPortraitUpsideDown = true;

//指定屏幕显示方向
Screen.orientation = ScreenOrientation.Landscape;
```

#### 静态方法

```c#
//设置分辨率 一般移动设备不使用
Screen.SetResolution(1920, 1080, false);
```



### Camera

#### Clear Flags

- skybox：主要用来做3d游戏
- solid color：纯色渲染，主要用来做2d游戏
- depthonly：深度渲染，与Depth结合使用。
- Don' clear：不清楚模式，游戏不会清楚前一帧屏幕。基本不会用。

#### Culling Mask

选择需要渲染的层级

#### Projection

- 选择Camera的透视方式。
- 透视模式和正交模式。
- 透视一般使用于3d游戏，正交一般用于2d游戏。具体还是看需求。

#### Clipping Planes

- 裁剪平面距离，可以调整Camera最近最远可以看到的距离。

#### Depth

- UI部分和3d部分分开Camera使用时，非常有用。

#### Target Texture

- 给Camera设置一张底片，在一张底片上进行渲染。
- 可以用在制作右下角的小地图。
- 在Project右键创建Render Texture

#### Occlusion Culling

- 让被挡住的内容不渲染，可以提高性能。

#### Viewport Rect（了解）

视口范围，屏幕上会绘制该Camera视图的位置，主要用于双Camera游戏，0-1相当于宽高百分比。

#### Redering path（了解）

渲染路径

#### Allow HDR（了解）

#### Allow MSAA（了解）

#### Allow Dynamic Resolution（了解）

#### Target Display（了解）



### Camera代码相关

#### 重要静态成员

##### 摄像机相关

```c#
//主摄像机的获取
//如果想通过这种方式快速获取摄像机，那么场景上必须有一个tag为MainCamera的摄像机。
print(Camera.main.name);

//获取摄像机的数量
print(Camera.allCamerasCount);

//得到所有摄像机
Camera[] allCamera = Camera.allCameras;
print(allCamera.Length);
```

##### 渲染相关委托

```c#
//摄像机剔除前，处理的委托函数
Camera.onPreCull += (c) =>
{

};

//摄像机 渲染前处理的委托
Camera.onPreRender += (c) =>
{

};

//摄像机 渲染后 处理的委托
Camera.onPostRender += (c) =>
{

};
```

#### 重要成员

##### 界面上的参数

- 界面上的参数都可以在Camera中获取到

```c#
//得到主摄像机对象 上的深度 进行设置
Camera.main.depth = 10;
```

##### 世界坐标转屏幕坐标

- 转换过后x和y对应的就是屏幕坐标，z对应的是这个3D物体离摄像机有多远
- 会用这个来做的功能，最多的就是头顶血条相关的功能

```c#
Vector3 v = Camera.main.WorldToScreenPoint(this.transform.position);
print(v);
```

##### 屏幕坐标转世界坐标

- 改变Z轴是因为如果不改，Z默认为0。
- 转换过去的世界坐标系的点永远都是一个点，可以理解为视口相交的焦点。
- 如果改变了Z，那么转换过去的世界坐标的点，就是相对于摄像机前方多少的单位的横截面上的世界坐标点
- 可以一些3d物体随着鼠标移动的功能。

```c#
Vector3 v = Input.mousePosition;
v.z = 5;
obj.position = Camera.main.ScreenToWorldPoint(v);
//print(Camera.main.ScreenToWorldPoint(v));
```

 

### 光源系统

#### 光源组件

##### 面板参数

###### Type

- 表示光源类型。

###### Color

- 颜色

###### Mode

- 光源模式。
- 实时光源（Realtime）、烘焙光源（Baked）、混合光源（Mixed）

###### Intensity

- 光源亮度

###### Shadow Type

- NoShadows（关闭阴影）、HardShadows（生硬阴影）、SoftShadows（柔和阴影）

###### Cookie

- 投影遮罩

###### Cookie Size（了解）



###### Draw Halo

- 球形光环开关。光晕的效果。

###### Flare

- 耀斑。
- 摄像机要看到耀斑效果的话，需要加组件“Flare Layer”

###### Culling Mask

- 剔除遮罩层，决定哪些层的对象受到该光源影响。

###### Rander Mode（了解）

- Auto
- Important，以像素为单位进行渲染，效果逼真，消耗大。可以用在汽车的灯光上。

##### 代码控制

面板上的参数已经够用了，主要是用一些成员变量。

```c#
light.intensity = 0.5f;
```

#### 光面板

![image-20231220151643484](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231220151643484.png)

##### 环境相关设置（Environment）

![image-20231220151409783](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231220151409783.png)

##### 其他设置（OtherSettings） 

![image-20231220151426637](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231220151426637.png)



### 物理系统之碰撞检测

碰撞、伤害检测。

#### 碰撞产生条件

- 两个物体产生碰撞的必要条件：两个物体都有碰撞器、至少有一个物体有刚体。
- 碰撞体结合刚体作用，只要有体积，又有力的作用，就可以模拟出碰撞。
- 拓展网格：所有的物体都是由一个又一个的面构成的，这些面称之为网格。

#### 刚体

刚体可以让物体有了力的作用，产生力的效果。

![image-20231220152614508](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231220152614508.png)

![image-20231220152637935](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231220152637935.png)

![image-20231220154121113](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231220154121113.png)

##### Augular Drag

旋转的阻力

##### Interpolate

插值运算。结合物理帧更新使用，物理帧过长可以改这里。

##### Discrete

离散检测，可能会发生子弹直接跳过物体。



#### 碰撞器

碰撞体可以理解为是用来体现3d物体的体积的。有了体积两个物体才能进行碰撞。

##### 组件参数

![image-20231220154720859](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231220154720859.png)

###### Is Trigger

- 是否为触发器。
- 可以让该碰撞体被物理引擎所忽略，用于碰撞事件。例如把一颗子弹做为触发器，那么该子弹会穿过射击的人，同时也会进行碰撞检测。

##### 常用碰撞器

![image-20231220154843223](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231220154843223.png)

##### 多种碰撞体组合

可以通过父子物体进行。

![image-20231220155133318](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231220155133318.png)

##### 网格碰撞器

- 性能消耗太高。
- 加了网格碰撞器的物体，如果需要用刚体，必须要勾选“Convex”才可以。

![image-20231220155450273](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231220155450273.png)

##### 环状碰撞器

- 轮胎碰撞器。
- 和刚体父对象配合使用，车身的质量要够大。

##### 地形碰撞器

效率太低，一般不用。



#### 物理材质

##### 创建物理材质

![image-20231220160930386](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231220160930386.png)

##### 物理材质参数

![image-20231220160913000](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231220160913000.png)



#### 碰撞检测函数

碰撞和触发响应函数属于特殊的生命周期函数，也是通过反射调用，会自动调用。

##### 物理碰撞响应函数

- Collision类型的参数，包含了碰到自己的对象的相关信息。
- 只要得到碰撞到的对象的任意一个信息，就可以得到它的所有信息

```c#
//碰撞触发接触时，会自动执行这个函数
private void OnCollisionEnter(Collision collision)
{
    //关键参数
    //碰撞到的对象碰撞器的信息
    collision.collider

    //碰撞对象的依附对象（GameObject）
    collision.gameObject

    //3.碰撞对象的依附对象的位置信息
    collision.transform

    //4.触碰点数相关
    collision.contactCount
    //接触点，具体的坐标
    ContactPoint[] pos = collision.contacts;

    print(this.name + "被" + collision.gameObject.name + "撞到了");
}

//碰撞结束分离时，会自动执行的函数
private void OnCollisionExit(Collision collision)
{
    print(this.name + "被" + collision.gameObject.name + "结束碰撞了");
}

//两个物体相互接触摩擦时，会不停的调用该函数
private void OnCollisionStay(Collision collision)
{
    print(this.name + "一直在和" + collision.gameObject.name + "接触");
}
```



##### 触发器检测响应函数

```c#
//触发开始的函数，当第一次接触时，会自动调用
protected virtual void OnTriggerEnter(Collider other)
{
    print(this.name + "被" + other.gameObject.name + "触发了");
}

//触发结束的函数，当水乳相融（交错）的状态结束时，会调用一次
private void OnTriggerExit(Collider other)
{
    print(this.name + "被" + other.gameObject.name + "结束水乳相融的状态了");
}

//当两个对象水乳相融（交错）的时候，会不停调用
private void OnTriggerStay(Collider other)
{
    print(this.name + "和" + other.gameObject.name + "正在水乳相融");
}
```

##### 补充

- 只要挂载的对象能和别的物体产生碰撞或者触发，那么对应的这6个函数就能够被响应
- 6个函数不是都得写，一般是根据需求来进行选择书写
- 如果是一个异形物体，刚体在父对象上，如果想通过子对象上挂脚本检测碰撞是不行的，必须挂载到这个刚体父对象上才行
- 物理碰撞和触发器响应的区别，有触发器的时候才能用触发器响应。
- 碰撞和触发器函数都可以写成虚函数，在子类去重写逻辑
- 一般会把想要重写的碰撞和触发函数，写成保护类型的，没有必要写成public，因为不会自己手动调用，都是Unity通过反射帮助我们自动调用的

#### 刚体加力

刚体自带添加力的方法

给刚体加力的目标是让其有一个速度，朝向某一个方向移动

```c#
//首先获取刚体组件
rigidBody = this.GetComponent<Rigidbody>();

//添加力
//相对世界坐标Z轴正方向加了一个力
//加力过后，对象是否停止移动由阻力决定的
//如果阻力为0，那给了一个力过后始终不会停止运动
rigidBody.AddForce(Vector3.forward * 10);
//即使有阻力也希望对象一直动，那就一直“推”
rigidBody.AddForce(Vector3.forward * 10);

//在世界坐标系方法中，对象相对于自己的面朝向动
rigidBody.AddForce(this.transform.forward * 10);
//相对本地坐标
rigidBody.AddRelativeForce(Vector3.forward * 10);


//添加扭矩力，让其旋转
//相对世界坐标
rigidBody.AddTorque(Vector3.up * 10);
//相对本地坐标
rigidBody.AddRelativeTorque(Vector3.up * 10);

//直接改变速度
//这个速度方向是相对于世界坐标系的 
//如果要直接通过改变速度来让其移动，一定要注意这一点，很少用。
rigidBody.velocity = Vector3.forward * 5;

//模拟爆炸效果
//所有希望产生爆炸效果影响的对象，都需要得到他们的刚体来执行这个方法，才能都有效果
//参数一：力的大小，参数二：爆炸中心，参数三：爆炸半径
rigidBody.AddExplosionForce(100, Vector3.zero, 10);
```



#### 力的几种模式

- AddForce方法第二个参数就是选择力的模式，主要是计算方式不同。
- 4种计算方式的不同，最终的移动速度就会不同

#####  动量定理

- Ft = mv
- v = Ft/m;
- F:力，t：时间，m:质量，v:速度

##### 模式一：Acceleration 

- 给物体增加一个持续的加速度，忽略其质量
- 例：
  v = Ft/m
  F:(0,0,10)
  t:0.02s
  m:默认为1
  v = 10*0.02/ 1 = 0.2m/s
  每物理帧移动0.2m/s*0.02 = 0.004m

##### 模式二：Force

- 给物体添加一个持续的力，与物体的质量有关
- 例：
  v = Ft/m
  F:(0,0,10)
  t:0.02s
  m:2kg
  v = 10*0.02/ 2 = 0.1m/s
  每物理帧移动0.1m/s*0.02 = 0.002m

##### 模式三：Impulse

- 给物体添加一个瞬间的力，与物体的质量有关,忽略时间 默认为1
- 例：
  v = Ft/m
  F:(0,0,10)
  t:默认为1
  m:2kg
  v = 10*1/ 2 = 5m/s
  每物理帧移动5m/s*0.02 = 0.1m

##### 模式四：VelocityChange

- 给物体添加一个瞬时速度，忽略质量，忽略时间
- 例：
  v = Ft/m
  F:(0,0,10)
  t:默认为1
  m:默认为1
  v = 10*1/ 1 = 10m/s
  每物理帧移动10m/s*0.02 = 0.2m

#### 力场脚本

Constant Force是unity提供的一个持续力的脚本。

#### 刚体的休眠

unity为节约性能， 会有刚体的休眠，在一定情况下不会进行计算了。

```c#
//取消休眠状态。 获取刚体是否处于休眠状态 
if (rigidBody.IsSleeping())
{
    //就唤醒它
    rigidBody.WakeUp();
}
#endregion
```



### 音效系统

#### 音频文件导入

##### 音效常用格式

![image-20231220171827606](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231220171827606.png)

##### 音频文件属性（面板）

![image-20231220171955163](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231220171955163.png)

 ![image-20231220190950484](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231220190950484.png)

#### 音频源脚本

##### 面板参数

![image-20231220191241531](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231220191241531.png)

![image-20231220191409146](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231220191409146.png)

####  代码控制

##### 播放停止

```c#
if( Input.GetKeyDown(KeyCode.P) )
 {
     //播放音效
     audioSource.Play();
     //延迟播放 填写的是秒数
     //audioSource.PlayDelayed(5);
 }
 if (Input.GetKeyDown(KeyCode.S))
 {
     //停止音效
     audioSource.Stop();
 }
 if( Input.GetKeyDown(KeyCode.Space) )
 {
     //暂停
     audioSource.Pause();
 }

 if( Input.GetKeyDown(KeyCode.X) )
 {
     //停止暂停 和暂停后 Play效果是一样的 都会继续播放现在的音效
     audioSource.UnPause();
 }
```

##### 检测音效播放完毕

如果希望某一个音效播放完毕后，想要做什么事情，那就可以在Update生命周期函数中不停的去检测它的属性

    //如果是false就代表播放完毕了
    if(audioSource.isPlaying)
    {
        print("播放中");
    }
    else
    {
        print("播放结束");
    }
    #endregion
动态控制音效播放

- 方法3中一个GameObject可以挂载多个音效源脚本AudioSource。
- 使用时要注意如果要挂载多个音效源脚本，那一定要自己管理他们、控制他们的播放、停止，不然没有办法准确的获取谁是谁

```c#
//1.直接在要播放音效的对象上挂载脚本 控制播放

//2.实例化挂载了音效源脚本的对象
//这种方法 其实用的比较少
Instantiate(obj);

//3.用一个AudioSource来控制播放不同的音效
AudioSource aus = this.gameObject.AddComponent<AudioSource>();
aus.clip = clip;
aus.Play();
```
#### 音频监听脚本

场景上有且只有一个“Audio Listener”才能听到音乐。

#### 麦克风输入

AudioClip，音效切片文件。

##### 获取设备麦克风信息

```c#
string[] strs = Microphone.devices;
for (int i = 0; i < strs.Length; i++)
{
    print(strs[i]);
}
```

##### 开始录制

```c#
//参数一：设备名 传空使用默认设备
//参数二：超过录制长度后 是否重头录制
//参数三：录制时长
//参数四：采样率，一般都是44100
private AudioClip clip;

if( Input.GetKeyDown(KeyCode.Space) )
{
    //clip用于存储录制的音频
    clip = Microphone.Start(null, false, 10, 44100);
}
```

##### 结束录制

```c#
if( Input.GetKeyUp(KeyCode.Space) )
{
    Microphone.End(null);
    //第一次去获取 没有才添加 
    AudioSource s = this.GetComponent<AudioSource>();
    if (s == null)
        s = this.gameObject.AddComponent<AudioSource>();
    s.clip = clip;
    s.Play();
}
```

##### 获取数据

获取音频数据用于存储或者传输规则：用于存储数组数据的长度是用声道数（clip.channels） * 剪辑长度（clip.samples）

```c#
    float[] f = new float[clip.channels * ];
    clip.GetData(f, 0);
    print(f.Length);
    #endregion
```

## 实践（坦克游戏项目）

### 场景的切换和退出

unity自带的SceneManger、Application类，可以对场景进行管理

```c
if( Input.GetKeyDown(KeyCode.Space) )
{
    //切换到场景2
    //直接 写代码 切换场景 可能会报错
    //原因是没有把该场景加载到场景列表当中
    SceneManager.LoadScene("Test2");

    //老版本的方法：用它不会报错，会有警告，可以切换场景 
    //Application.LoadLevel("Test2");
}

if( Input.GetKeyDown(KeyCode.Escape) )
{
    //执行这句代码 就会退出游戏
    //但是 在编辑模式下没有作用
    //一定是发布游戏过后 才有用
    Application.Quit();
}
```

### 鼠标隐藏、锁定、设定

unity提供了Cursor类，可以对鼠标进行设置

光标图片设置时，要记得改成Cursor类型

```c#
//隐藏鼠标
Cursor.visible = true;

//锁定鼠标
//None：不锁定
//Locked：锁定鼠标，会被限制在屏幕的中心点，不仅会被锁定、还会被隐藏。可以通过ESC键摆脱编辑模式下的锁定
//Confined：限制在窗口范围内
Cursor.lockState = CursorLockMode.Confined;

//设置鼠标图片
//参数一：光标图片
//参数二：偏移位置 相对图片左上角
//参数三：平台支持的光标模式（硬件或软件），一般用自动模式就行
Cursor.SetCursor(tex, Vector2.zero, CursorMode.Auto);
```

### 随机数

在unity中要使用随机数的话，直接用引擎命名空间的随机数即可。

```c#
//Unity当中 的Random类 此Random(Unity)非彼Random（C#）
//使用随机数 int重载 规则是 左包含 右不包含
//0~99之间的数
int randomNum = Random.Range(0, 100);
print(randomNum);
//float重载 规则是 左右都包含
float randomNumF = Random.Range(1.1f, 99.9f);

//C#中的随机数
System.Random r = new System.Random();
r.Next(0, 100);
```

### 自带委托

```c#
//C#的自带委托
System.Action ac = () =>
{
    print("123");
};

System.Action<int, float> ac2 = (i, f) =>
{

};

System.Func<int> fun1 = () =>
{
    return 1;
};

System.Func<int,string> fun2 = (i) =>
{
    return "123";
};

//Unity的自带委托
UnityAction uac = () =>
{

};

UnityAction<string> uac1 = (s) =>
{
    
};

```

### 模型资源导入

![image-20240316143337142](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240316143337142.png)

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240316143422108.png" alt="image-20240316143422108" style="zoom:50%;" />

![image-20240316143718832](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240316143718832.png)





# unity基础





# <center>---------数据持久化---------</center>

![image-20231222162646262](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231222162646262.png)

![image-20231222162721300](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20231222162721300.png)

# PlayerPrefbs

PlayerPrefs是Unity提供的可以用于存储读取玩家数据的公共类

## 基本用法

PlayerPrefs的数据存储，类似于键值对存储，一个键对应一个值，提供了存储3种数据的方法 int float string。

键: string类型 
值：int float string 对应3种API

### 存储相关

```c#
//Set相关方法，只会把数据存到内存里。
//当游戏结束时，Unity会自动把数据存到硬盘中。
//如果游戏不是正常结束的，而是崩溃，数据是不会存到硬盘中的。
PlayerPrefs.SetInt("myAge", 18);
PlayerPrefs.SetFloat("myHeight", 177.5f);
PlayerPrefs.SetString("myName", "akkkkk东软");

//Save方法就会马上存储到硬盘中
PlayerPrefs.Save();

//PlayerPrefs是有局限性的，只能存3种类型的数据
//想要存储别的类型的数据，可以降低精度，或者上升精度来进行存储
bool sex = true;
PlayerPrefs.SetInt("sex", sex ? 1 : 0);

//如果不同类型用同一键名进行存储 会进行覆盖
PlayerPrefs.SetFloat("myAge", 20.2f);
```

### 读取相关

运行时只要Set了对应键值对，即使没有马上存储Save在本地，也能够读取出信息。

```c#
//int
int age = PlayerPrefs.GetInt("myAge");
print(age);
//如果找不到myAge对应的值,就会返回函数的第二个参数(默认值)
//默认值就是在得到没有的数据的时候，可以来进行基础数据的初始化
age = PlayerPrefs.GetInt("myAge", 100);
print(age);

//float
float height = PlayerPrefs.GetFloat("myHeight", 1000f);
print(height);

//string
string name = PlayerPrefs.GetString("myName");
print(name);

//判断数据是否存在
if( PlayerPrefs.HasKey("myName") )
{
    print("存在myName对应的键值对数据");
}
```

### 删除数据

```c#
//删除指定键值对
PlayerPrefs.DeleteKey("myAge");
//删除所有存储的信息
PlayerPrefs.DeleteAll();
```

## 数据存储位置

### Windows

HKCU\Software\[公司名称]\[产品名称] 项下的注册表中

其中公司和产品名称是 在“Project Settings”中设置的名称。

```c#
//运行 regedit
//HKEY_CURRENT_USER
//SOFTWARE
//Unity
//UnityEditor
//公司名称
//产品名称
```

### Android

 /data/data/包名/shared_prefs/pkg-name.xml 

### IOS

 /Library/Preferences/[应用ID].plist

## 数据唯一性

PlayerPrefs中不同数据是由key决定的，不同的key决定了不同的数据

同一项目中，如果不同数据key相同会造成数据丢失，要保证数据不丢失就要建立一个保证key唯一的规则。



# 实践（数据管理类型PlayerPrefbsDataMgr）

## 反射知识补充

![image-20240316165656368](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240316165656368.png)

![image-20240226234548369](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240226234548369.png)

```
Type的IsAssignableFrom()函数，返回是否能装
```

![image-20240226234613060](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240226234613060.png)

```
Type的GetGenericArguments()函数，获取泛型类型
```

## 需求分析

![image-20240226234932172](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240226234932172.png)

![image-20240226235009767](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240226235009767.png)

## 大致思路和套路

变量的种类很多，而PlayerPrefbs只支持三种简单类型的直接存储和读取（float、int和string）。

- 将所有传入需要存储、读取的变量都视作是一个未知的自定义类，用父类object存储。利用反射的知识。
- Type类型可以获得类的所有信息，包含字段（成员变量）、属性和方法等。
- FieldInfo类型就是用于存储字段（变量）的。包含了该字段（成员变量）的类型名、变量名。
- 以此，可以

![image-20240316165246963](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240316165246963.png)

```c#
//（假设要存储的数据是obect data）

//第一步：获取传入数据对象的所有字段
//获得传入的数据对象的Type信息
Type dataType = date.getType();
//通过Type得到字段（FieldInfo类型）
FieldInfo[] infos = dataType.GetFields();

//第二步：定义key的规则

//第三步：遍历字段，进行存储
FieldInfo info;
for (int i=0;i<infos.Length;i++)
{
    //字段（FieldInfo类型）中存有字段的类型和名字
    //类型：info.FieldType.Name（比如：Int32）
    //名字：info.Name(比如：age)
    info = infos[i];
    
    //根据拼接规则生成keyname
    keyname = xxxx;
    
    //生成keyvalue（获得值）GetValue：在data里面获取info这个字段的值传入keyvalue。
    keyvalue = info.GetValue(data);
    
    //得到键和值后，继续存储
    //注意：PlayerPrefbs只支持三种基本类型的直接读写。我们会有其他需求，因此才定义了SaveValue，专门用于处理单个字段的存值问题。
    
}


```









## 存储方面

步骤：

- 通过万物之父object类型，存储未知类型（某种自定义类）data。
- 创建Type的dataType，表示data变量的类型，通过GetType()方法可以获得其类型。
- 通过反射中的GetFields()方法，获得data类中的所有成员变量。
- 遍历处理，存储所有成员变量。

### 一般数据类型

int，float，string直接调用PlayerPrebs的API即可。

bool等其他一般数据类型，可以自行利用API进行存储，定一个规则即可。

### List数据类型

通过判断其父类是否为某一特定/特殊的类，可以辨别其是否为特定类型。

在List类的定义中，继承了IList的接口。目前判断的类中，只有List继承了IList，可以通过判断父类是否为IList，就可以判断是否为List类型。

### dictionary数据类型

与List同理。

### 自定义类（其他类）数据类型

除了前面提到的基础数据类型，则认为是自定义类的数据类型

## 读取方面



## 加密思路

注意：单机游戏加密只是提高别人修改你数据的门槛，只要别人获取到你的源代码、知道你的加密规则，一切都没有任何意义。但是对于一般玩家来说几乎是不可能的事情。

### 找不到

把存在硬盘上的内容放在一个不容易找到的地方。

多层文件夹包裹

名字辨识度低

但是对于PlayerPrefs不太适用因为位置已经固定了我们改不了

### 看不懂

让数据的Key和Value让别人看不懂，俗称加密

为Key和Value加密

### 解不出

不让别人获取到你加密的规则就解不出来了

## 生成资源包

  







# <center>------------UI系统------------</center>

UI系统的主要学习内容

1.UI控件的使用

2.UI控件的事件响应

3.Ul的分辨率自适应

# UI系统之GUI

GUI全称即时模式游戏用户交互界面（IMGUI），在Unity中一般简称为GUI，它是一个代码驱动的UI系统。

- **作为程序员的调试工具，创建游戏内调试工具，他是每帧更新的。不要用它为玩家制作UI功能。**
- 为脚本组件创建自定义检视面板
- 创建新的编辑器窗口和工具以拓展Unity本身（一般用作内置游戏工具）

## 工作原理

在继承MonoBehaviour的脚本中的特殊函数里，调用GUI提供的方法，类似生命周期函数 

OnGUI是每帧更新的。

```c#
private void OnGUI()
{
    //在其中书写 GUI相关代码 即可显示GUI内容
}
```

- 注意：
- 它每帧执行 相当于是用于专门绘制GUI界面的函数
- 一般只在其中执行GUI相关界面绘制和操作逻辑
- 该函数 在 OnDisable之前  LateUpdate之后执行
- 只要是继承Mono的脚本 都可以在OnGUI中绘制GUI

## 重要参数

GUI公共类中提供的都是静态函数，直接调用即可。

每一种控件都有多种重载，都是各个参数的排列组合，必备的参数内容是位置信息和显示信息。

-   位置参数：Rect参数 x y位置 w h尺寸
-   显示文本：string参数
-   图片信息：Texture参数
-   综合信息：GUIContent参数
-   自定义样式：GUIStyle参数

## GUI内容

### 文本控件

```c#
GUI.Label()
```

```c#
//基本使用
GUI.Label(new Rect(0, 0, 100, 20), "唐老狮欢迎你");
GUI.Label(rect, tex);
//综合使用
GUI.Label(rect1, content);
//可以获取当前鼠标或者键盘选中的GUI控件 对应的 tooltip信息
Debug.Log(GUI.tooltip);
//自定义样式
GUI.Label(new Rect(0, 0, 100, 20), "唐老狮欢迎你", style);
```

style的参数含义如下：

![image-20240306105453413](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240306105453413.png)

### 按钮控件

```c#
GUI.Button()
GUI.RepeatButton()
```

button的style里面可以设置放上去、按下和抬起的样式。

基本使用、综合使用等使用方式，和前面文本控件一样，就是参数的排列组合

```c#
public Rect btnRect;
public GUIContent btnContent;
public GUIStyle btnStyle;

private void OnGUI()
{
    //在按钮范围内按下鼠标再抬起鼠标，才算一次点击，返回true
    if (GUI.Button(btnRect, btnContent, btnStyle))
    {
        //处理我们按钮点击的逻辑
        Debug.Log("按钮被点击");
    }

    //在长按按钮范围内按下鼠标，就会一直返回true
    if( GUI.RepeatButton(btnRect, btnContent) )
    {
        Debug.Log("长按按钮被点击");
    }
}
```



### 多选框

```
GUI.Toggle()
```

```c#
private bool isSel;
private bool isSel2;


private void OnGUI()
{
    //普通样式
    //GUI.Toggle()有个bool的返回值，返回值为选中状态（是否选中）
    isSel = GUI.Toggle(new Rect(0, 0, 100, 30), isSel, "效果开关");

    //自定义样式点击图标时，点击图标的宽高其实是一整个相应位置的宽高，因此如果单纯的调图标的宽高，这可能会导致部分区域无法响应。
    //1.修改固定宽高（fixedWidth和fixedHeight）
    //2.修改从GUIStyle边缘到内容起始处的空间（padding）
    //3.是否选中的样式可以更换一下，以看出效果。
    isSel2 = GUI.Toggle(new Rect(0, 40, 100, 30), isSel2, "音效开关", style);
}
```



### 单选框

单选框是基于多选框的实现

关键：通过一个int标识来决定是否选中 

```c#
private int nowSelIndex = 1;
private void OnGUI()
{
    if (GUI.Toggle(new Rect(0, 100, 100, 30), nowSelIndex == 1, "选项一"))
    {
        nowSelIndex = 1;
    }
    if (GUI.Toggle(new Rect(0, 140, 100, 30), nowSelIndex == 2, "选项二"))
    {
        nowSelIndex = 2;
    }
    if (GUI.Toggle(new Rect(0, 180, 100, 30), nowSelIndex == 3, "选项三"))
    {
        nowSelIndex = 3;
    }
}
```



### 输入框

```c#
GUI.TextField()
GUI.PasswordField()
```

- TextField()参数二：显示内容的text，string类型（即inputStr，类中名字是“text”）
- TextField()参数三：最大输入字符串的长度（即“5”）

```c#
private string inputStr = "";
private string inputPW = "";
private void OnGUI()
{
    //不断把输入的内容赋值，才能改变inputStr
    inputStr = GUI.TextField(new Rect(0, 0, 100, 30), inputStr, 5);
    
    inputPW = GUI.PasswordField(new Rect(0, 50, 100, 30), inputPW, '*');
}
```



### 拖动条

```c#
GUI.HorizontalSlider()
GUI.VerticalSlider()
```

```c#
// 当前的值
private float nowValue = 0.5f;
private void OnGUI()
{
    // 最小值 left；最大值 right
    // 水平拖动条
    nowValue = GUI.HorizontalSlider(new Rect(0, 100, 100, 50), nowValue, 0, 1);
    
    //竖直拖动条
    nowValue = GUI.VerticalSlider(new Rect(0, 150, 50, 100), nowValue, 0, 1);
}
```



### 图片绘制

```c#
GUI.DrawTexture(texPos, tex, ScaleMode, alpha, wh);
```

- ScaleMode

  - ScaleAndCrop:也会通过宽高比来计算图片 但是 会进行裁剪

  - ScaleToFit：会自动根据宽高比进行计算 不会拉变形 会一直保持图片完全显示的状态
  - StretchToFill:始终填充满你传入的 Rect范围

- alpha是用来控制图片是否开启透明通道的

- imageAspect，自定义宽高比 ，如果不填默认为0，就会使用图片原始宽高  

```c#
public Rect texPos;
public Texture tex;
public ScaleMode mode = ScaleMode.StretchToFill;
public bool alpha = true;
public float wh = 0;
private void OnGUI()
{
    GUI.DrawTexture(texPos, tex, mode, alpha, wh);
}
```



### 框的绘制

效果就是增加一个底，然后可以绘制固定的内容。

使用情况很少。

```c#
GUI.Box()
```

```c#
public Rect texPos;
private void OnGUI()
{
    GUI.Box(texPos, "");
}
```



### 工具栏

工具栏可以帮助我们根据不同的返回索引 来处理不同的逻辑

```c#
GUI.Toolbar()
```

```c#
private int toolbarIndex = 0;
private string[] toolbarInfos = new string[] { "选项一", "选项二", "选项三" };
private void OnGUI()
{
    toolbarIndex = GUI.Toolbar(new Rect(0, 0, 200, 30), toolbarIndex, toolbarInfos);
    
    //进一步处理逻辑
    switch (toolbarIndex)
    {
        case 0:
            break;
        case 1:
            break;
        case 2:
            break;
    }
}
```



### 选择网格

```
GUI.SelectionGrid()
```

xCount 表示水平方向最多显示的按钮数量。对比工具栏（toolbar）多了一个参数 。

```c#
private int toolbarIndex = 0;
private string[] toolbarInfos = new string[] { "强化", "进阶", "幻化" };
private int selGridIndex = 0;
private void OnGUI()
{
    selGridIndex = GUI.SelectionGrid(new Rect(0, 50, 200, 60), selGridIndex, toolbarInfos, 1);
}
```



### 分组

```c#
GUI.BeginGroup();
XXXX
GUI.EndGroup();
```

```c#
public Rect groupPos;
public Rect scPos;
public Rect showPos;
private Vector2 nowPos;
private string[] strs = new string[] { "123", "234", "222", "111" };
private void OnGUI()
{
    // 用于批量控制控件位置 
    // 可以理解为包裹着的控件加了一个父对象 
    // 可以通过控制分组来控制包裹控件的位置
    GUI.BeginGroup(groupPos);
    
    GUI.Button(new Rect(0, 0, 100, 50), "测试按钮");
    GUI.Label(new Rect(0, 60, 100, 20), "Label信息");
    
    GUI.EndGroup();
}
```



### 滚动列表

```c#
nowPos = GUI.BeginScrollView(scPos, nowPos, showPos);
XXXX
GUI.EndScrollView();
```

- scPos决定的是可见范围和尺寸
- nowPos为滚动的文本框，当前相对于初始的所在位置。
- showPos决定具体内容的大小

![image-20240306114814793](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240306114814793.png)

```c#
public Rect scPos;
public Rect showPos;
private Vector2 nowPos;
private string[] strs = new string[] { "123", "234", "222", "111" };
private void OnGUI()
{
    nowPos = GUI.BeginScrollView(scPos, nowPos, showPos);

    GUI.Toolbar(new Rect(0, 0, 300, 50), 0, strs);
    GUI.Toolbar(new Rect(0, 60, 300, 50), 0, strs);
    GUI.Toolbar(new Rect(0, 120, 300, 50), 0, strs);
    GUI.Toolbar(new Rect(0, 180, 300, 50), 0, strs);

    GUI.EndScrollView();
}
```

### 窗口

#### 窗口

```c#
GUI.Window(id,Rect,DrawWindow,"")
```

- id 是窗口的唯一ID，不要和别的窗口重复
- 委托参数DrawWindow，用于 绘制窗口用的函数，传入即可

```c#
private Rect dragWinPos = new Rect(400, 400, 200, 150);
private void OnGUI()
{
    //id可以在一个函数中去处理多个窗口的逻辑，通过id去区分他们
    GUI.Window(1, new Rect(100, 100, 200, 150), DrawWindow, "测试窗口");
    GUI.Window(2, new Rect(100, 350, 200, 150), DrawWindow, "测试窗口2");
}

private void DrawWindow(int id)
{
    switch (id)
    {
        case 1:
            GUI.Button(new Rect(0, 30, 30, 20), "1");
            break;
        case 2:
            GUI.Button(new Rect(0, 30, 30, 20), "2");
            break;
        case 3:
            GUI.Button(new Rect(0, 30, 30, 20), "3");
            break;
        case 4:
            //该API 写在窗口函数中调用 可以让窗口被拖动
            //传入Rect参数的重载 作用 
            //是决定窗口中哪一部分位置 可以被拖动
            //默认不填 就是无参重载 默认窗口的所有位置都能被拖动
            GUI.DragWindow(new Rect(0,0,1000,20));
            break;
    }
    
}
```

#### 模态窗口

模态窗口可以让该其它控件不在有用

可以理解该窗口在最上层 其它按钮都点击不到了，只能点击该窗口上控件

```
GUI.ModalWindow()
```

```c#
private void OnGUI()
{
    GUI.ModalWindow(3, new Rect(300, 100, 200, 150), DrawWindow, "模态窗口");
}

private void DrawWindow(int id)
{
    switch (id)
    {
        case 1:
            GUI.Button(new Rect(0, 30, 30, 20), "1");
            break;
        case 2:
            GUI.Button(new Rect(0, 30, 30, 20), "2");
            break;
        case 3:
            GUI.Button(new Rect(0, 30, 30, 20), "3");
            break;
    }
    
}
```

#### 拖动窗口

DragWindow是写在窗口函数中调用的，可以让窗口被拖动

```c#
GUI.DragWindow()
```

- 传入的Rect参数起重载作用，可以决定窗口中哪一部分位置可以被拖动。
- 默认不填（无参重载）默认窗口的所有位置都能被拖动。
- 填入的Rect表示鼠标只有在这个区域内，才可把窗口进行拖动。

```c#
private Rect dragWinPos = new Rect(400, 400, 200, 150);
private void OnGUI()
{
    dragWinPos = GUI.Window(4, dragWinPos, DrawWindow, "拖动窗口");
}

private void DrawWindow(int id)
{
    switch (id)
    {
        case 1:
            GUI.Button(new Rect(0, 30, 30, 20), "1");
            break;
        case 2:
            GUI.Button(new Rect(0, 30, 30, 20), "2");
            break;
        case 3:
            GUI.Button(new Rect(0, 30, 30, 20), "3");
            break;
        case 4:
            GUI.DragWindow(new Rect(0, 0, 1000, 20));
            break;
    }

}
```




### 自定义皮肤

GUIStyle是可以自定义的样式变量，可以在右侧属性列表中进行设置。

#### 全局颜色

```c#
public GUIStyle style;
private void OnGUI()
{
    //全局的着色颜色（会影响背景和文本颜色）
    GUI.color = Color.red;

    //文本着色颜色（会和全局颜色相乘，从而导致可能不是想要的颜色。）
    //一般来说如果想要改变文本，那么就不要设置全局颜色
    GUI.contentColor = Color.yellow;
    GUI.Button(new Rect(0, 0, 100, 30), "测试按钮");

    //背景元素着色颜色（会和全局颜色相乘）
    //同理
    GUI.backgroundColor = Color.red;
    GUI.Label(new Rect(0, 50, 100, 30), "测试按钮");
    GUI.color = Color.white;
    GUI.Button(new Rect(0, 100, 100, 30), "测试按钮", style);
}
```

#### 整体皮肤样式

unity自带GUISkin类型，是GUI的皮肤文件，可以预设样式的参数。

可以帮助我们整套的设置自定义样式，相对单个控件设置GUIStyle要方便一些。

```c#
public GUISkin skin;
private void OnGUI()
{
    GUI.skin = skin;
    //虽然设置了皮肤，但是绘制时如果使用GUIStyle参数，皮肤就没有。
    GUI.Button(new Rect(0, 0, 100, 30), "测试按钮");

    GUI.skin = null;
    GUI.Button(new Rect(0, 50, 100, 30), "测试按钮2");
}
```

### GUILayout自动布局

一般是不用来制作游戏的UI内容，主要用于编辑器开发。

可以自动布局，方便快速的搭建UI。

可以配合GUI.BeginGroup等使用。

```c#
private void OnGUI()
{
    //控件的固定宽高
    GUILayout.Width(300);
    GUILayout.Height(200);
    
    //允许控件的最小宽高
    GUILayout.MinWidth(50);
    GUILayout.MinHeight(50);
    
    //允许控件的最大宽高
    GUILayout.MaxWidth(100);
    GUILayout.MaxHeight(100);
    
    //允许或禁止水平拓展
    GUILayout.ExpandWidth(true);//允许
    GUILayout.ExpandHeight(false);//禁止
    GUILayout.ExpandHeight(true);//允许
    GUILayout.ExpandHeight(false);//禁止
}
```

# 实践（GUI的封装优化）

## 编辑模式下执行脚本

一般情况下，GUI的内容在编辑模式下是无法运行看出效果的。此时在脚本最前面，加个特性既可。

加特性后，unity就能在编辑模式下，通过反射实现效果。

```c#
[ExecuteAlways]
```

## 九宫格布局概念

我们始终无法改变屏幕原点在屏幕左上角，以及控件的原点在他自身的左上角事实。因此通过计算来得出我们想要的位置，以此到达分辨率自适应的效果。

- 相对屏幕位置：屏幕原点在左上角
- 中心点偏移位置：控件原点在控件的左上角
- 偏移位置：固定在某个点后，相对于该点的偏移值

![image-20240315131655519](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240315131655519.png)

![image-20240315131911672](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240315131911672.png)



## 控件位置信息类



## 控件绘制基类



## 控制所见即所得

用特性，在编辑模式下执行脚本即可。

## 控制控件对象绘制顺序







# <center>------------InputSystem------------</center>

## InputSystem的一些设置

InputSystem在资源商店导入即可。

InputSystem导入后，会默认关闭老的输入系统。

选择InputSystem和老InputManager的启用情况：File——>Build Setting——>Player Setting——>Other——>Active Input Handling（可以同时启用也可以只启用其中之一,每次启用后会重启Unity）

注意：两套输入系统都开启的话，调用Api的时候，运行后可能会报错。

## 代码检测输入

### 键盘输入

- 任意键：keyBoard.anyKey
- 抬起：wasPressedThisFrame
- 长按：wasReleasedThisFrame
- 按下：isPressed

```c#
void Start()
{
    //获取目前活跃（进行交互了）的键盘按键
	Keyboard keyBoard = Keyboard.current;
}

void Update()
{
    //空格键 当前帧 是否按下
    if (Keyboard.current.spaceKey.wasPressedThisFrame)
    {
        print("空格键按下");
    }

    //判断D键是否释放
    if (Keyboard.current.dKey.wasReleasedThisFrame)
    {
        print("D键抬起");
    }

    //判断空格是否一直处于按下状态
    if (Keyboard.current.spaceKey.isPressed)
    {
        print("空格按下状态");
    }

    //任意键按下了
    if (Keyboard.current.anyKey.wasPressedThisFrame)
    {
        print("任意键按下");
    }
    
    //给keyboard对象中的文本输入事件添加委托函数，可以获得每次输入的内容
    keyBoard.onTextInput += (c) =>
    {
        print("通过lambda表达式" + c);
    };
    keyBoard.onTextInput += TextInput;
    keyBoard.onTextInput -= TextInput;
}
```



### 鼠标输入

- 鼠标左键：mouse.leftButton
- 鼠标右键：mouse.rightButton
- 鼠标中键：mouse.middleButton
- 鼠标 向前向后键：mouse.forwardButton、mouse.backButton

```c#
void Start()
{
    //获取当前鼠标设备（需要引用命名空间）
    Mouse mouse = Mouse.current;
}

void Update()
{
    if (Mouse.current.leftButton.wasPressedThisFrame)
    {
        print("鼠标左键按下");
    }

    //抬起
    if (Mouse.current.leftButton.wasReleasedThisFrame)
    {
        print("鼠标左键抬起");
    }
    //长按
    if (Mouse.current.rightButton.isPressed)
    {
        print("鼠标右键长按");
    }
    
    //获取当前鼠标位置
    mouse.position.ReadValue();
    print(Mouse.current.position.ReadValue());
    
    //得到鼠标两帧之间的一个偏移向量（鼠标相对于上一帧的偏移向量）。作用：鼠标左右的正负值不一样，可以利用这个来做一些旋转等的功能。
    mouse.delta.ReadValue();
    print(Mouse.current.delta.ReadValue());

    //鼠标中间 滚轮的方向向量
    mouse.scroll.ReadValue();
    print(Mouse.current.scroll.ReadValue());
}
```



### 触屏输入



```c#
void Start()
{
    #region 获取当前触屏设备
    Touchscreen ts = Touchscreen.current;
    //由于触屏相关都是在移动平台或提供触屏的设备上使用
    //所以在使用时最好做一次判空
    if (ts == null)
        return;
    #endregion

    #region 得到触屏手指信息
    //得到触屏手指数量
    print(ts.touches.Count);
    //得到单个触屏手指
    ts.touches[1]
    //得到所有触屏手指
    foreach (var item in ts.touches)
    {

    }
    #endregion

    #region  手指按下、抬起、长按、点击
    //获取指定索引手指
    TouchControl tc = ts.touches[0];
    //按下 抬起
    if (tc.press.wasPressedThisFrame)
    {

    }
    if (tc.press.wasReleasedThisFrame)
    {

    }
    //长按
    if (tc.press.isPressed)
    {

    }

    //点击手势
    if (tc.tap.isPressed)
    {

    }

    //获得连续点击次数
    print(tc.tapCount);

    #endregion

    #region 手指位置等相关信息
    //位置
    print(tc.position.ReadValue());
    //第一次接触时位置
    print(tc.startPosition.ReadValue());
    //接触区域大小
    tc.radius.ReadValue();
    //偏移位置（偏移向量）
    tc.delta.ReadValue();

    //得到当前手指的状态（阶段）（开始点击、结束点击等）
    UnityEngine.InputSystem.TouchPhase tp = tc.phase.ReadValue();
    switch (tp)
    {
        //无
        case UnityEngine.InputSystem.TouchPhase.None:
            break;
        //开始接触
        case UnityEngine.InputSystem.TouchPhase.Began:
            break;
        //移动
        case UnityEngine.InputSystem.TouchPhase.Moved:
            break;
        //结束
        case UnityEngine.InputSystem.TouchPhase.Ended:
            break;
        //取消
        case UnityEngine.InputSystem.TouchPhase.Canceled:
            break;
        //静止
        case UnityEngine.InputSystem.TouchPhase.Stationary:
            break;
        default:
            break;
    }
    #endregion
}
```



### 手柄输入

市面上的手柄大致有三种，任天堂、索尼和微软这三套。

![image-20240320234330607](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240320234330607.png)

```c#
void Start()
{
    #region 知识点一 获取当前手柄
    Gamepad gamePad = Gamepad.current;
    //最好判空
    if (gamePad == null)
        return;
    #endregion

    #region 知识点二 手柄摇杆
    //摇杆方向
    //左摇杆
    print(gamePad.leftStick.ReadValue());
    //右摇杆
    print(gamePad.rightStick.ReadValue());

    //左摇杆leftStickButton，右摇杆rightStickButton
    if (gamePad.leftStickButton.wasPressedThisFrame)
    {

    }
    if (gamePad.leftStickButton.wasReleasedThisFrame)
    {

    }
    if (gamePad.leftStickButton.isPressed)
    {

    }
    #endregion

    #region 知识点三 手柄方向键
    //对应手柄上4个方向键 上下左右
    //gamePad.dpad.left
    //gamePad.dpad.right
    //gamePad.dpad.up
    //gamePad.dpad.down
    if (gamePad.dpad.left.wasPressedThisFrame)
    {

    }
    if (gamePad.dpad.left.wasReleasedThisFrame)
    {

    }
    if (gamePad.dpad.left.isPressed)
    {

    }
    #endregion

    #region 知识点四 手柄右侧按键
    //（通用）
    //Y、△：gamePad.buttonNorth
    //A、X：gamePad.buttonSouth
    //X、□：gamePad.buttonWest
    //B、○：gamePad.buttonEast

    //（对应手柄名字、不建议这么写）
    //○：gamePad.circleButton
    //△：gamePad.triangleButton
    //□：gamePad.squareButton
    //X：gamePad.crossButton
    //x：gamePad.xButton
    //a：gamePad.aButton
    //b：gamePad.bButton
    //Y：gamePad.yButton
    #endregion

    #region 知识点五 手柄中央按键
    //其他手柄中央的东西都是和手柄自身系统有关的，与游戏无关
    //中央键
    //gamePad.startButton
    //gamePad.selectButton
    #endregion

    #region 知识点六 手柄肩部按键
    //左上右上 肩部键位
    //左右前方肩部键
    //gamePad.leftShoulder
    //gamePad.rightShoulder

    //左右后方触发键
    //gamePad.leftTrigger
    //gamePad.rightTrigger
    #endregion
}

void Update()
{
    //左摇杆
    //print(Gamepad.current.leftStick.ReadValue());
    //右摇杆
    //print(gamePad.rightStick.ReadValue());

    if (Gamepad.current.leftStickButton.wasPressedThisFrame)
    {
        print("左摇杆按下");
    }
    if (Gamepad.current.leftStickButton.wasReleasedThisFrame)
    {
        print("左摇杆抬起");
    }
    if (Gamepad.current.leftStickButton.isPressed)
    {
        print("左摇杆长按");
    }

    if (Gamepad.current.dpad.left.wasPressedThisFrame)
    {
        print("左方向键按下");
    }
    if (Gamepad.current.dpad.left.wasReleasedThisFrame)
    {
        print("左方向键抬起");
    }
    if (Gamepad.current.dpad.left.isPressed)
    {
        print("左方向键长按");
    }

    if (Gamepad.current.buttonNorth.wasPressedThisFrame)
    {
        print("上方按键 三角形键(PS)按下");
    }

    if (Gamepad.current.startButton.wasPressedThisFrame)
    {
        print("开始键按下");
    }
    if (Gamepad.current.selectButton.wasPressedThisFrame)
    {
        print("选择键按下");
    }


    if (Gamepad.current.leftShoulder.wasPressedThisFrame)
    {
        print("左侧肩部前方键");
    }


    if (Gamepad.current.leftTrigger.wasPressedThisFrame)
    {
        print("左侧肩部后方键");
    }
}
```



### 其他输入设备

对于我们没有细讲的设备，平时在开发中不是特别常用。如果想要学习他们的使用，最直接的方式就是看官方的文档、或者直接进到类的内部查看具体成员，通过查看变量名和方法名即可了解使用方式。

注意：新输入系统的设计初衷就是想提升开发者的开发效率，不提倡写代码来处理输入逻辑

学了配置文件相关知识后，都是通过配置文件来设置监听（监视窃听）的输入事件类型，只需要把工作重心放在输入触发后的逻辑处理。



## InputAction

- InputAction是InputSystem帮助我们封装的输入动作类。
- 主要作用是不需要我们通过写代码的形式来处理输入，直接在Inspector窗口编辑想要处理的输入类型。
- 当输入触发时，只需要把精力花在输入触发后的逻辑处理上。
- 用法是在想要用于处理输入动作的类中 申明对应的InputAction类型的成员变量（注意：需要引用命名空间UnityEngine.InputSystem）

### 参数相关

#### “齿轮”设置

![image-20240320235731247](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240320235731247.png)

Actinos参数：

![image-20240320235747615](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240320235747615.png)

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240320235812583.png" alt="image-20240320235812583" style="zoom:80%;" />

Interactions参数：

![image-20240321000000564](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240321000000564.png)

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240321000030026.png" alt="image-20240321000030026" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240321000122566.png" alt="image-20240321000122566" style="zoom:50%;" />

Prcessors参数：

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240321000302900.png" alt="image-20240321000302900" style="zoom:80%;" />

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240321000327939.png" alt="image-20240321000327939" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240321000619976.png" alt="image-20240321000619976" style="zoom:50%;" />

#### “+号”设置

添加的是输入的类型

![image-20240321000826382](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240321000826382.png)

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240321000912755.png" alt="image-20240321000912755" style="zoom:80%;" />

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240321002153267.png" alt="image-20240321002153267" style="zoom:80%;" />

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240321003045998.png" alt="image-20240321003045998" style="zoom:80%;" />

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240321003527362.png" alt="image-20240321003527362" style="zoom:80%;" />

### InputAction的使用

```c#
//示例变量定义。
//InputAction原本无法直接看出InputAction的名字，可以用特性继续显示。
[Header("Binding")]
public InputAction move;
[Header("1D Axis")]
public InputAction axis;
[Header("2D Vector")]
public InputAction vector2D;
[Header("3D Vector")]
public InputAction vector3D;
[Header("Button With One")]
public InputAction btnOne;

void Start()
{
    #region InputAction的使用
    //1.启用输入检测
    move.Enable();

    //2.操作监听相关
    //开始操作
    move.started += TestFun;

    //真正触发
    move.performed += (context) =>
    {
        print("触发事件调用");
        //当前状态
        //没有启用：Disabled
        //等待：Waiting
        //开始：Started
        //触发：Performed
        //结束：Canceled
        //context.phase
        print(context.phase);
        
        //一些常用的参数
        //获得动作行为信息（就是这个InputAction的名字）
        print(context.action.name);

        //获得控件(设备)信息
        print(context.control.name);

        //获取值
        //context.ReadValue<float>

        //获得持续时间
        print(context.duration);

        //开始时间
        print(context.startTime);
    };

    //结束操作
    move.canceled += (context) =>
    {
        print("结束事件调用");
    };

    //3.关键参数 CallbackContext（可以在这个参数里获得以下的信息）
    //当前状态

    //动作行为信息 

    //控件信息

    //获取值

    //持续时间

    //开始时间


    axis.Enable();
    vector2D.Enable();
    vector3D.Enable();

    btnOne.Enable();
    btnOne.performed += (context) =>
    {
        print("组合键触发");
    };

    #endregion

    #region 特殊输入设置
    //1.Input System 基础设置（一些默认值设置）
    //2.设置特殊输入规则
    #endregion
}
```

### InputSystem Package的设置

![image-20240321003956529](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240321003956529.png)

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240321003911564.png" alt="image-20240321003911564" style="zoom: 80%;" />

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240321003930105.png" alt="image-20240321003930105" style="zoom:80%;" />

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240321003941885.png" alt="image-20240321003941885" style="zoom:80%;" />



### 配置文件

- 输入系统中提供了一种输入配置文件，可以理解它是InputAction的集合
- 在一个文件中编辑多个InputAction的信息
- 里面记录了想要处理的行为和动作（也就是InputAction的相关信息），
- 可以在其中自己定义 InputAction（比如：开火、移动、旋转等），然后为这个InputAction关联对应的输入动作，之后将该配置文件和PlayerInput进行关联
- PlayerInput会自动帮助我们解析该文件。当触发这些InputAction输入动作时会以分发事件的形式通知我们执行行为
- 该文件本质就是将这些信息写成了Json文件

![image-20240321011951192](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240321011951192.png)

ActionMaps：

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240321012036707.png" alt="image-20240321011951192" style="zoom: 67%;" />

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240321014044967.png" alt="image-20240321011951192" style="zoom: 50%;" />

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240321084554571.png" alt="image-20240321084554571" style="zoom:50%;" />

### 配置文件与C#脚本结合

```c#
private PlayerInputStudy.PlayerTest player;
private void Start()
{
    //new对象
    player = new PlayerInputStudy.PlayerTest();

    //激活他
    player.Enable();

    player.Player.Jump.performed += Jump_performed;
    player.Player.Fire.performed += Fire_performed;

}
```

## PlayerInput

- PlayerInput是InputSystem提供的专门用于接受玩家输入来处理自定义逻辑的组件。

- 主要工作原理：

  1.配置输入文件（InputActions文件）
  2.通过PlayerInput关联配置文件，它会自动解析该配置文件
  3.关联对应的响应函数，处理对应逻辑

- 好处：

  不需要自己进行相关输入的逻辑书写
  通过配置文件即可配置想要监听的对应行为
  让我们专注于输入事件触发后的逻辑处理

### 参数解释

![image-20240321091119035](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240321091119035.png)

### 行为执行模式解释（Behavior）

- 一般使用后两种方式

#### Send Messages

- 在自定义脚本中申明名为 "On+行为名" 的函数

- 没有参数或者参数类型为InputValue

- 将该自定义脚本挂载到PlayerInput依附的对象上

- 当触发对应输入时，会自动调用函数

- 有默认的3个和设备相关的函数可以调用：

  1.设备注册(当控制器从设备丢失中恢复并再次运行时会触发)：OnDeviceRegained(PlayerInput input)
  2.设备丢失（玩家失去了分配给它的设备之一，例如，当无线设备耗尽电池时）：OnDeviceLost(PlayerInput input)
  3.控制器切换：OnControlsChanged(PlayerInput input)

```c#
public void OnMove(InputValue value)
{
	print("Move");
}

public void OnMove(InputValue value)
{
	print("Look");
	print(value.get<Vector2>());
}

public void OnMove(InputValue value)
{
	print("Fire");
}

public void OnDeviceLost(PlayerInput input)
{
	print("设备丢失");
}

public void OnDeviceRegained(PlayerInput input)
{
	print("设备注册");
}

public void OnControlsChanged(PlayerInput input)
{
	print("控制器切换");
}
```



#### Broadcast Messages

- 基本和SendMessage规则一致
- 唯一的区别是，自定义脚本不仅可以挂载在PlayerInput依附的对象上，还可以挂载在其子对象下

#### Invoke Unity Events

- 该模式可以让我们在Inspector窗口上通过拖拽的形式关联响应函数
- 但是注意响应函数的参数类型需要为 InputAction.CallbackContext

```c#
public void MyFire(InputAction.CallbackContext context)
{
    print("开火1");
}

public void MyMove(InputAction.CallbackContext context)
{
    print("移动1");
}

public void MyLook(InputAction.CallbackContext context)
{
    print("Look1");
}
```

#### Invoke C Sharp Events

```c#
void start()
{
    //1.获取PlayerInput组件
    PlayerInput input = this.GetComponent<PlayerInput>();
    //2.获取对应事件进行委托函数添加
    input.onDeviceLost += OnDeviceLost;
    input.onDeviceRegained += OnDeviceRegained;
    input.onControlsChanged += OnControlsChanged;
    input.onActionTriggered += OnActionTrigger;
    //3.当触发输入时会自动触发事件调用对应函数
}

public void OnActionTrigger(InputAction.CallbackContext context)
{
    switch (context.action.name)
    {
        case "Fire":
            //输入阶段的判断 触发阶段 才去做逻辑
            if(context.phase == InputActionPhase.Performed)
                print("开火");
            break;
        case "Look":
            print("看向");
            print(context.ReadValue<Vector2>());
            break;
        case "Move":
            print("移动");
            print(context.ReadValue<Vector2>());
            break;
    }
}
```

#### C#代码使用

```c#
input.currentActionMap["Move"].ReadValue<Vector2>()
```



## PlayerInputManager

PlayerInputManager 组件主要是用于管理本地多人输入的输入管理器，它主要管理玩家加入和离开

### 参数解释

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240321141039739.png" alt="image-20240321141039739" style="zoom:67%;" />

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240321141125472.png" alt="image-20240321141125472" style="zoom:67%;" />

### 使用

注意设置的预设体中要含有InputSystem组件。

场景中其他的对象挂载了InputSystem组件（与预设体的冲突的话）的话，最好全部失活。

## UGUI的配合使用

### InputSystem对UI的支持

- 新输入系统InputSystem不支持IMGUI（GUI）
  注意：编辑器代码不受影响
- 如果当前激活的是InputSystem，那么OnGUI中的输入判断相关内容不会被触发。
- 必须要选择Both或者只激活老输入系统，InputManager才能让OnGUI中内容有用
- 新输入系统支持UGUI（平时使用的画布UI），但是需要使用新输入系统输入模块（Input System UI Input Module）

### InputSystem与UGUI

前面说了，新输入系统支持UGUI，但需要使用新输入系统输入模块（Input System UI Input Module）

#### 输入模块参数相关

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240321150150460.png" alt="image-20240321150150460" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240321150605285.png" alt="image-20240321150605285" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240321150839137.png" alt="image-20240321150839137" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240321150909396.png" alt="image-20240321150909396" style="zoom:50%;" />

### VR相关中使用新输入系统注意事项

在VR项目中使用新输入系统配合UGUI使用，需要在Canvas对象上添加Tracked Device Raycaster组件

### 多人游戏使用多套UI情况

如果同一设备上的多人游戏，每个人想要使用自己的一套独立UI。那么需要将EventSystem中的EventSystem组件替换为Multiplayer Event System组件

与EventSystem组件不同，可以在场景中同时激活多个MultiplayerEventSystem。这样可以有多个玩家，每个玩家都有自己的InputSystemUIInputModule和MultiplayerEventSystem组件，每个玩家都可以有自己的一组操作来驱动自己的UI实例。

如果正在使用PlayerInput组件，还可以设置PlayerInput以自动配置玩家的InputSystemUIInputModule以使用玩家的操作。MultilayerEventSystem组件的属性与事件系统中的属性相同

MultiplayerEventSystem组件还添加了一个playerRoot属性，可以将其设置为一个游戏对象。该游戏对象包含此事件系统应在其层次结构中处理的所有UI可选择项

### On-Screen组件相关

On-Screen组件可以模拟UI和用户操作的交互。

使用方式是在该UI上增加对应组件，通过绑定后，即可通过该UI进行操作左右上下、跳跃等（屏幕模拟器）。

On-Screen Button：按钮交互

/On-Screen Stick：摇杆交互

### 更多内容

可查看官方文档了解更多新输入系统和UI配合使用的相关内容：https://docs.unity3d.com/Packages/com.unity.inputsystem@1.2/manual/UISupport.html

## InputDebug

InputDebug是输入调试器，可以通过输入调试窗口检测输入相关信息

当我们的输入不按预期工作时，可以通过它来排查问题

### 打开InputDebug窗口

Window(窗口)->Analysis(分析)->Input Debugger(输入调试器)

PlayerInput组件->Open Input Debugger

### 窗口上的信息

<img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240321160513299.png" alt="image-20240321160513299" style="zoom:50%;" />

（此处赶进度没有继续听下去，有需要再回头来）



## 练习

### 1.

![image-20240320232955442](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240320232955442.png)

```c#
public class Exercises : MonoBehaviour
{
    public Material redMaterial;
    private Material normalMaterial;
    private GameObject obj = null;

    private int scaleFactor = 1;
    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        //鼠标左键按下 才进行射线检测
        if( Mouse.current.leftButton.wasPressedThisFrame )
        {
            RaycastHit info;
            if (Physics.Raycast(Camera.main.ScreenPointToRay(Mouse.current.position.ReadValue()), out info))
            {
                obj = info.collider.gameObject;
                normalMaterial = obj.GetComponent<MeshRenderer>().material;
                obj.GetComponent<MeshRenderer>().material = redMaterial;
            }
            else
            {
                //还原材质球
                if(obj != null)
                    obj.GetComponent<MeshRenderer>().material = normalMaterial;
                normalMaterial = null;
                obj = null;
            }
        }
        

        if(obj != null)
        {
            if (Keyboard.current.numpadPlusKey.wasPressedThisFrame ||
            Keyboard.current.equalsKey.wasPressedThisFrame)
            {
                scaleFactor += 1;
                obj.transform.localScale = Vector3.one * scaleFactor;
            }

            if (Keyboard.current.numpadMinusKey.wasPressedThisFrame ||
                Keyboard.current.minusKey.wasPressedThisFrame)
            {
                scaleFactor -= 1;
                if (scaleFactor < 1)
                    scaleFactor = 1;
                obj.transform.localScale = Vector3.one * scaleFactor;
            }
        }
    }
}
```

### 2、

![image-20240321004127135](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240321004127135.png)



```c#
public class Exercise2 : MonoBehaviour
{
    [Header("移动系统")]
    public InputAction Move;
    [Header("跳跃系统")]
    public InputAction Jump;
    [Header("开火系统")]
    public InputAction Fire;

    private Rigidbody body;
    private Vector3 dir;

    public GameObject BulletPrefab;

    private void Start()
    {
        body = GetComponent<Rigidbody>();

        Move.Enable();

        Jump.Enable();
        Jump.performed += Jump_performed;

        Fire.Enable();
        Fire.performed += Fire_performed;
    }

    private void Fire_performed(InputAction.CallbackContext obj)
    {
        //鼠标位置的射线检测
        RaycastHit info;
        if (Physics.Raycast(Camera.main.ScreenPointToRay(Mouse.current.position.ReadValue()),out info))
        {
            //屏幕获取的是一个平面的点，那么子弹飞出去就是贴着xz平面（即地面）的。
            //在平面上的向量再叠加向y轴（垂直于地面）的向量，即可实现斜向上的子弹发色效果。
             
            //得到子弹飞出去的单位向量。
            Vector3 point = info.point;
            point.y = this.transform.position.y;    //得到终点向量
            Vector3 dir = point - this.transform.position;  //向量=终点-起点
            dir.Normalize(); //单位化，得到单位向量

            //创建子弹飞出去
            Instantiate(BulletPrefab, this.transform.position,Quaternion.LookRotation(dir));    //Quaternion.LookRotation(dir)是通过unity得到dir的四元数角度
             
        }
    }

    private void Jump_performed(InputAction.CallbackContext obj)
    {
        body.AddForce(Vector3.up * 200);
    }

    private void Update()
    {
        //Move.ReadValue得到的是x，y的V2对象，而我们移动的时候，是在x，z平面上。因此需要对方向进行转换
        //AddForce对刚体施加力，需要传入的是V3对象，因此定义中间变量dir来表示转化后，移动目的的坐标。
        dir = Move.ReadValue<Vector2>();
        dir.z = dir.y;
        dir.y = 0;
        body.AddForce(dir);

    }
}
```

## 综合实践

### 获取任意键输入的信息

```c#
//如果用Call按键盘会报错，但是也能正常执行
//用CallOnce只会执行一次，但是不会报错
InputSystem.onAnyButtonPress.CallOnce((control) =>
{
    print(control.path);
    print(control.name);
});
```

### 通过Json数据加载配置文件

（赶进度没看）

### 实践内容（改键功能）

![image-20240321161455304](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_unityimage-20240321161455304.png)



# --------------TimeLine--------------

## 拓展方法



步骤一：脚本一编写轨道，继承TrackAsset（轨道资产），

步骤二：脚本一使用TrackBindingType（轨道绑定类型）特性来标记需要绑定的成员（比如Light、Text等）

步骤四：脚本一添加TrackClipType注释（轨道和片段产生联系，让片段能够添加到轨道上）





步骤三：脚本二编写片段，继承PlayableAsset（可播放资产）、实现ITimelineClipAsset（主要是实现支持特性）



步骤五：脚本三编写片段行为（如何操控该对象），继承PlayableBehaviour。（轨道不支持混合就直接重写ProcessFrame函数，在里面编写控制光源）



步骤六：（若要轨道能够混合）脚本三继承PlayableBehaviour



TrackAsset代表了Tlmeline里的一类轨道









# ------------算法------------

# A星寻路算法

大多数时候是用在2d游戏中的。unity的3d可以用网格寻路。





























