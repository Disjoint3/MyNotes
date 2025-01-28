# ------------进阶、补充

# <center>InputSystem</center>

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



# TimeLine

## 拓展方法



步骤一：脚本一编写轨道，继承TrackAsset（轨道资产），

步骤二：脚本一使用TrackBindingType（轨道绑定类型）特性来标记需要绑定的成员（比如Light、Text等）

步骤四：脚本一添加TrackClipType注释（轨道和片段产生联系，让片段能够添加到轨道上）





步骤三：脚本二编写片段，继承PlayableAsset（可播放资产）、实现ITimelineClipAsset（主要是实现支持特性）



步骤五：脚本三编写片段行为（如何操控该对象），继承PlayableBehaviour。（轨道不支持混合就直接重写ProcessFrame函数，在里面编写控制光源）



步骤六：（若要轨道能够混合）脚本三继承PlayableBehaviour



TrackAsset代表了Tlmeline里的一类轨道

# ScriptableObject

## 概述

![image-20240613162428448](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/06/13/20240613162435.png)

![image-20240613162509574](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/06/13/20240613162509.png)

![image-20240613162531662](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/06/13/20240613162531.png)

![image-20240613162607077](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/06/13/20240613162607.png)

![image-20240613162635877](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/06/13/20240613162635.png)

## 数据文件的创建

**自定义ScriptableObject数据容器**

![image-20240613163349755](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/06/13/20240613163349.png)

**根据CreateAssetMenu创建数据文件**

![image-20240613165250812](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/Img/2024/06/13/20240613165250.png)

方法一：为类添加CreatAssetMenu。

- 注意类要继承CreateAssetMenu

方法二：



XXXXX



## 应用

### 配置数据





### 复用数据





### 数据带来的多态行为















































































