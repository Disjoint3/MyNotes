# <center>---------数据持久化</center>

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

  

# XML

![image-20240522165246790](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/11/09/20241109164123.png)

![image-20240522165410180](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/11/09/20241109164123-1.png)

## XML文件格式

### XML基本语法

![image-20240522165847631](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/11/09/20241109164123-2.png)

#### 注释

```xml
<!--注释-->
<!--
注释
-->
```

#### 固定内容（编码）

![image-20240522170424108](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/11/09/20241109164123-3.png)

```xml
<!--固定内容代表XML的版本 使用的编码-->
<?xml version="1.0" encoding="UTF-8"?>
```

#### 基本语法

XML是树状结构，一定要有根结点。

![image-20240522170748892](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/11/09/20241109164123-4.png)

#### 基本规则

![image-20240522170823520](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/11/09/20241109164123-5.png)

### XML属性

#### 属性语法

![image-20240522171023078](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/11/09/20241109164123-6.png)

![image-20240522171129777](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/11/09/20241109164123-7.png)

### 语法错误

![image-20240522171319849](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/11/09/20241109164123-8.png)

## C#读取存储XML

### XML文件存储位置

- 只读不写的XML文件可以放在Resources或者StreamingAssets文件夹下
- 动态存储的XML文件放在Application.persistentDataPath 路径下

### 读取XML文件信息

通过XmlDocument读取xml文件 有两个API

```c#
XmlDocument xml = new XmlDocument();

//1.直接根据xml字符串内容 来加载xml文件
//存放在Resorces文件夹下的xml文件加载处理
TextAsset asset = Resources.Load<TextAsset>("TestXml");
print(asset.text);
//通过这个方法 就能够翻译字符串为xml对象
xml.LoadXml(asset.text);

//2.是通过xml文件的路径去进行加载
xml.Load(Application.streamingAssetsPath + "/TestXml.xml");
```

读取元素和属性

节点信息：XmlNode 单个节点信息类

节点列表信息：XmlNodeList 多个节点信息类

以下图为例：

![image-20240523210607315](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/23/20240523210614.png)

```c#
//获取xml当中的根节点
XmlNode root = xml.SelectSingleNode("Root");
//再通过根节点 去获取下面的子节点
XmlNode nodeName = root.SelectSingleNode("name");
//如果想要获取节点包裹的元素信息 直接 .InnerText
print(nodeName.InnerText);

//获取尖括号中的属性  
XmlNode nodeItem = root.SelectSingleNode("Item");
//第一种方式 直接 中括号获取信息
print(nodeItem.Attributes["id"].Value);
print(nodeItem.Attributes["num"].Value);
//第二种方式 
print(nodeItem.Attributes.GetNamedItem("id").Value);
print(nodeItem.Attributes.GetNamedItem("num").Value);

//获取一个节点下的同名节点的方法
XmlNodeList friendList = root.SelectNodes("Friend");
//遍历方式一：迭代器遍历
foreach (XmlNode item in friendList)
{
    print(item.SelectSingleNode("name").InnerText);
    print(item.SelectSingleNode("age").InnerText);
}
//遍历方式二：通过for循环遍历
// 通过XmlNodeList中的 成员变量 Count可以得到 节点数量
for (int i = 0; i < friendList.Count; i++)
{
    print(friendList[i].SelectSingleNode("name").InnerText);
    print(friendList[i].SelectSingleNode("age").InnerText);
}

```

 **总结：**

![image-20240523211434124](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/23/20240523211434.png)

### 存储XML文件信息

存储位置：

![image-20240523211710236](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/23/20240523211710.png)

 假设路径：

```c#
string path = Application.persistentDataPath + "/PlayerInfo2.xml";
print(Application.persistentDataPath);
```

关键类：

- XmlDocument 用于创建节点 存储文件
- XmlDeclaration 用于添加版本信息
- XmlElement 节点类

以下图为例：

![image-20240523212512464](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/05/23/20240523212512.png)

```c#
//存储有5步
//1.创建文本对象
XmlDocument xml = new XmlDocument();

//2.添加固定版本信息
//这一句代码 相当于就是创建<?xml version="1.0" encoding="UTF-8"?>这句内容
XmlDeclaration xmlDec = xml.CreateXmlDeclaration("1.0", "UTF-8", "");
//创建完成过后 要添加进入 文本对象中
xml.AppendChild(xmlDec);

//3.添加根节点
XmlElement root = xml.CreateElement("Root");
xml.AppendChild(root);

//4.为根节点添加子节点
//加了一个 name子节点
XmlElement name = xml.CreateElement("name");
name.InnerText = "唐老狮";
root.AppendChild(name);

XmlElement atk = xml.CreateElement("atk");
atk.InnerText = "10";
root.AppendChild(atk);

XmlElement listInt = xml.CreateElement("listInt");
for (int i = 1; i <= 3; i++)
{
    XmlElement childNode = xml.CreateElement("int");
    childNode.InnerText = i.ToString();
    listInt.AppendChild(childNode);
}
root.AppendChild(listInt);

XmlElement itemList = xml.CreateElement("itemList");
for (int i = 1; i <= 3; i++)
{
    XmlElement childNode = xml.CreateElement("Item");
    //添加属性
    childNode.SetAttribute("id", i.ToString());
    childNode.SetAttribute("num", (i * 10).ToString());
    itemList.AppendChild(childNode);
}
root.AppendChild(itemList);

//5.保存
xml.Save(path);
```

### 修改XML文件信息

```c#
//1.先判断是否存在文件
if( File.Exists(path) )
{
    //2.加载后 直接添加节点 移除节点即可
    XmlDocument newXml = new XmlDocument();
    newXml.Load(path);

    //修改就是在原有文件基础上 去移除 或者添加
    //移除
    XmlNode node;// = newXml.SelectSingleNode("Root").SelectSingleNode("atk");
    //这种是一种简便写法 通过/来区分父子关系
    node = newXml.SelectSingleNode("Root/atk");
    //得到自己的父节点
    XmlNode root2 = newXml.SelectSingleNode("Root");
    //移除子节点方法
    root2.RemoveChild(node);

    //添加节点
    XmlElement speed = newXml.CreateElement("moveSpeed");
    speed.InnerText = "20";
    root2.AppendChild(speed);

    //改了记得存
    newXml.Save(path);
}
```



# Json

## Json配置

注释：和C#中注释方式一致

- 1.双斜杠 //注释内容
- 2.斜杠加星号 /*注释内容 */

## 语法和注意

![image-20241109161921683](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/11/09/20241109163638.png)

![image-20241109163558335](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/11/09/20241109163627.png)









































































