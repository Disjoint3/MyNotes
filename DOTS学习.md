# DOTS项目创建

## 渲染管线

unity的项目必须是可编程渲染管线，比如URP、UDRP等。

## package包

[com.unity.entities](https://docs.unity3d.com/Packages/com.unity.entities@latest):渲染我们的entity所需要的的包。下载这个源码包匹配的文档，比官网的要更准确，更匹配你的版本。（但搞不定翻译。。。还是网页的吧）

[com.unity.entities.graphics](https://docs.unity3d.com/Packages/com.unity.entities.graphics@latest):就是我们主要的ECS 相关的工具包: Entity,ECS,Job System, Burst

<u>**com.unity.Physics**</u>: 负责我们的游戏里面的ECS下的物理引擎;



## 设置

（1.0.16版本）

![image-20240802153841463](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/08/09/20240809174855.png)



## DOTS开发应用

 DOTS的时候，你普通的开发也是可以的，所以我们普通开发与DOTS的开发，是可以共存的。

GameObject与Entity我们也是可以共存的UI开发，网络开发传统方式，大量重复的性能要求高得游戏体，我们可以使用DOTS得entity来做



## 注解

注解：給一个类型做一些注释对象，到时候我们可以读取得到

在做反射得时候，我们得类型，会生成一个Type对象：t。所以这个注解得对象，就会被记录在t对象实例里面，你可以通过t对象实例，获取
注解得实例。

比如：

```c#
class EntityObjct : Attribute
{
    public EntityObjct(string name)
    {

    }
}

// 注解 + 装饰器;
// 注解:給一个类型做一些注释对象，到时候我们可以读取得到
[EntityObjct("MyEntiy")]
public class GameEntiyObject
{

}
```

[EntityObject("MyEntiy")]：

1. new EntityObject("MyEntiy");对象出来
2. 把这个对象记录到我们的GameEntiyObject的Type t实例的Attribute中。

**作用**

- 可以扫描特定的类
- 创建对象实例等



## 托管对象与非托管对象

托管对象:垃圾回收器直接会回收的对象

非托管对象:垃圾回收器不管的，你要自己释放

unsafe code: 使用指针



## ECS源码

ECS源码可以直接从package里得到，直接阅读方便学习。

# DOTS核心机制与概述

**面向数据的编程**

**D**(Data)**O**(0riented)**T**(Technology)**S**(stack)

程序 =数据结构 +算法

**面向对象的编程**

【数据+方法】，类与对象

## ECS

ECS的开发方式就是30年前的C语言的方式

- Entity: 实体
- Component: 组件数据;
- System: 代码算法 + 多线程
- Entity+ Component,处理我们数据相关，System就是算法，内存布局与多线程

### Entity（实体）

Entity中文翻译为实体，但这个实体是一个<u>概念</u>。

Entity表示程序中具有自己数据集的离散物体。（个人理解，这里的实体可算是一个对象？）

Entity相当于是component的容器，由多个component组合而成。

### Component（组件）

Component<u>**包含**</u>System（系统）可以读写的Entity的数据。

![image-20240802184402038](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/08/09/20240809174855-1.png)*<u>（对于加粗的“包含”：这里文档用的是“include”。这个包含说明组件≠数据，那它到底是个什么？？？？暂时很疑惑)</u>*



IComponentDate接口内并没有任何方法，使用这个接口可以将一个结构标记成component。这种component只能<u>**容纳**</u>非托管的数据（非托管就是要自行释放），并且也可以容纳（其他的）方法（但文档中说最好还是视为纯数据）。
![image-20240802184347959](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/08/09/20240809174855-2.png)
<u>*（对于加粗的“容纳”：文档用的是“contain”。根据查询的英文，个人擅自理解成容纳，个人理解是component作为一个”容器“可以”装“非托管的数据。*</u>



【英文补充】

contain和include：

- contain是一种内部包含，所包含的事物不一定是主语的同类事物；include是同种事物之间的包含，宾语所指的人或物与主语是同类，有包含和被包含的关系。
- contain着重"内有"，作及物动词是"包含；包括；能容纳，能装入。
- include着重"被包含者只是整体中的一部分"。



*（课堂笔记）*

1、Component是存放我们Entity数据的载体

2、Component里面的这个数据是给Sytem的算法来进行读写的;

3、定义一个ComponentData/component 

```c#
struct Component:lComponentData
//用来标记这个类型是一个Component
```

4、如果我们的组件ComponetData继承自IComponentData，那么他里面数据成员只能是非托管数据类型;（int、float这些），可以带一些方法。

5、如果你想要创建一个可以托管的ComponentData,你就把这个ComponentData定义成class就可以了

6、![image-20240809145220176](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/08/09/20240809174855-3.png)
假设：
EntityA:Comp1,comp2+comp3...
（特定组合，记为ArchType1）（chunk16kib）
EntityB:Comp5,Comp6+...
（特定组合，记为ArchType2)

若EntityA这种类型的Entity有10个，那么可以从16kib的chunk分配10个archetype_size给这10个Entity，直到这个chunk被分配完。
对于EntityB，则有新的chunk来分配其内存给这种类型的Entity。



7、几种类型的Component;



8、编写第一个System;搞一个托管 mananged System;





### System（系统）

System提供Component数据从当前状态向下一状态的逻辑。*（个人理解就是处理数据的动态逻辑）*例如，更新所有移动Entity的位置，处理方法预先定好，可能是速度乘时间间隔等。

![image-20240803153042481](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/08/09/20240809174855-4.png)



*(课堂笔记)*

1、System是提供一种代码逻辑, 改变我们的组件的数据状态（从一个状态到另外一个状态）这里的状态可以认为是ComponentData数据内容。

说白了就是System可以读取ComponentData的数据的内容。

2、System的算法程序是运行在main thread里面的, System.Update的方法每一帧执行一次

System是通过一个System Group这个体系来决定它调用的顺序

System是在System group下

3、创建一个基于托管的System：定义一个 class, 然后继承SystemBase
非托管的System：定义一个struct，然后继承Isystem;

4、可以重写三个接口:  
OnUpdate: 每帧会调用一次
OnCreate: 创建的时候调用一次
OnDestroy: 销毁的时候调用一次;

5、一个System只能处理同一个世界（World）的Entity。一个系统只能处理一个世界中的实体，因此一个系统与一个特定的世界相关联。
可以通过system对象.World属性，可以获得当前这个system对象所在的World世界

6、定义了一个System,但是没有去自己创建实例，仍然可以用，这是因为默认情况下， 启动的时候会为每个system与SystemGroup创建一个实例出来。

默认启动的时候，会创建一个默认的世界World，同时会默认创建3个system groups：
InitializationSystemGroup
SimulationSystemGroup
PresentationSystemGroup

默认情况下，我们创建出来的System实例，会放到 SimulationSystemGroup这个分组下。可以使用使用[UpdateInGroup]这个注解来制定你这个System放到那个分组。

7、要关闭这个默认，可以用宏定义的操作：#UNITY_DISABLE_AUTOMATIC_SYSTEM_BOOTSTRAP. 

8、可以使用的System类型。

9、SystemGroup

SystemGroup:可以有很多个System,同时还可以有孩子SystemGroup

SystemGroup也有Update，你可以来重写,来调用孩子相关的update,来定制你调用的顺序;

10、System Window

可以使用SystemsWindow 去查看我们的每个世界的system的update的顺序



11、编写第一个System;搞一个托管 mananged System;



12、编写第一个System;搞一个托管 mananged System;













### World（世界）

World是Entity的集合体，Entity的ID号在自身的World中是唯一的。

World（世界）有一个专门的EntityManager，负责高效的分配与释放相关的entity。EntityManager可以创建、销毁和修改该世界中实体们的方法。

World中的Entity由多个的Component（组件）组合在一起，这多个Component类型会有一个Archetype。这个Archetype决定了Component的内存排布。

World存放许多的Entity，同时管理所有的System，所有的算法迭代处理当前世界里面的Entity们。



#### World初始化

- 默认情况下，Unity会创建一个（默认的）World实例，并将每个系统都添加到这个默认世界中。

- 若要手动添加系统到默认World中，要实现ICustomBootstrap接口。

- 若连默认World都要手动控制，可以用宏定义来：

  #UNITY_DISABLE_AUTOMATIC_SYSTEM_BOOTSTRAP_RUNTIME_WORLD：禁用默认运行时世界的生成

  #UNITY DISABLE AUTOMATIC SYSTEM BOOTSTRAP EDITOR WORLD：禁用默认编辑器世界的生成.

  #UNITY DISABLE AUTOMATIC SYSTEM BOOTSTRAP：禁用两个默认世界的生成。

创建完世界和系统后，将世界的更新插入PlayLoop中。

Unity使用WorldFlags在编辑器中创建专门的世界。







### Archetype（原型）

Archetype是component们组合的描述，不同的组合表示不同的Archetype。

Entity由多个component组合而成，这些组合的类型称为Archetype，Archetype决定了component的内存存放方式。

可以基于Archetype进行内存排布和内存管理。

相当于Entity减少、增加一个component，其Achetype也会改变。

![image-20240803152421700](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/08/09/20240809174855-5.png)

![image-20240803162629800](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/08/09/20240809174855-6.png)

### ECS伪代码

![image-20240803153745468](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/08/09/20240809174855-7.png)



### 总结

#### Entity与ComponentData

Unity传统方法：

- gameObject+component，每个component都是独立的对象。

ECS：

- Entity: 世界中的我们的对象实例, Entity 的数据是存放在ComponentData里面、
- Entity [componentData1, componentData2]，不同的component决定一个新的类型，在内存中，将所有的component排在一起。

- Entity 本身不负责存数据，可以看作轻量级的GameObject。
- 数据是存放在一块内存里面，而所有组件组合成的一个连续内存块。连续的内存块包含了所有的组件数据。

DOTS效率高的原因之一：将对象变成Entity模式，每个对象要用到的数据在内存中连续排布在一起，能够大幅度提高CPU cache命中率。













## Job System

前面的ECS流程中，游戏引擎的Update迭代主要是在mainThread里面。

Job System引入多线程，可以用不同的线程来发挥计算机的多核优势。

Job System迭代机制中，每个System的Update都用不同线程来迭代。主要使用是线程池来迭代System，需要使用的数据也是component的数据。

DOTS中编写的JobSystem代码就是多线程开发代码。



## EntityQuery

EntityQuery是查询Component数据的机制。

通过EntityQuery可以到Archtype管理的所有Component组合的内存块中，将某种特定类型的Component数据取出来，放在一个连续的内存块中。

比如：想要将Entity里面的Transform数据取出，通过EntityQuery，可以得到一个Array[T1,T2,T3]。





## Burst工具链

传统Unity：.net代码--->il2cpp--->cpp code--->编译器编译

Burst工具链：.net代码--(基于LLVM虚拟机机制)--->native code（使用了MMX“单指令多数据集”指令）--->cpp代码--->编译器编译

这里面，使用LLVM的方法替代传统的il2cpp方法，生成native code。这个native code使用的是MMX指令集，可以并行处理，提高cpu的性能。



【MMX指令集】

MMX指令集实质是一种SIMD数据处理方式(单指令流，多数据流)，由intel公司开发，它允许CPU同时对2-4个甚至8个数据进行并行处理

add 指令:同时可以把多组数据，一起通过add指令，来完成加法

内存拷贝，一次拷贝8个字节，内存拷贝性能都会变得成倍的i提升;



# DOTS的SubScene

## SubScene机制

Unity传统的场景和ESC的机制会冲突，因此引入SubScene替代传统的Scene。

传统的Scene：

- GameObject + 组件（Mono）

SubScene：

- 可以正常的像普通的开发模式一样，在SubScene里面来添加 的GameObject、MonoBehaviour
- Unity将subscene里面的物体，一个一个的烘培出来，转成ECS 模式
- <u>可以自己定义Baker，加一个ECS 的Component到这个Entity上</u>



## 创建SubScene





## 添加自定义ComponentData

subscene中， Unity 自动启动bake，Blake出来后，所有的对象会变成Entitys。

Entity包含一些ComponentData，bake过程中，自带组件会被自动转过来。

Authoring：负责将普通的物体转换成Entity的代码。



Step1:新建一个Authoring组件类(C#脚本)

Step2:要求组件类定义一个Bake，让系统通过这个Bake的模式转换数据。（SubScene中，类实例化后通过bake转换为ECS世界的东西）

