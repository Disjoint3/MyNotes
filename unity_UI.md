# <center>------------UI系统</center>

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















































