![image-20221222163858277](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212221638322.png)

## AppL的组成

AppL中最重要的就是SWC了，而SWC与其他SWC通信需要接口，每个SWC中又由runnable组成，所以AppL主要的组成就分下面三部分：

1. **应用软件组件（SWC  Software Component）**
1. **AutoSAR接口（Ports）和连接器（Connector）**
1. **可运行实体（Runnable Entity）**


![bg](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212221957414.png)



## 一、举个例子

**汽车顶灯的控制**：

![img](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212221958204.jpeg)

车内的顶灯一般有三种模式：

1. 常闭的模式
2. 常开的模式
3. 随车开关而开关的模式

好了，那么我们来捋一捋。

- 首先肯定是需要传感器（包括图上的和车门上的）
- 处理单元
- 执行器（图上的车顶灯）。

假如就以下图为简单逻辑而言：有左右两个车门，左右两个车灯，一个开关传感器。这里我们分配了7个SWC，将传感器、处理单元和执行器都分的很细，且这里并非由一个ECU控制。

## ![在这里插入图片描述](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212221958032.png)二、SWC的通信

我们将上图的SWC整理一下，做成大家容易理解的横向一排的样式，如下：

![在这里插入图片描述](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212222007003.png)SWC之间的通信是通过独立的一个层级进行交互，我们称其为虚拟功能总线（VFB)，也就是RTE的实现。该总线是意义上的片内外通信的结合体，取了个名字叫虚拟功能总线，其实际就是分两部分：

1. **在片内**就是通过RTE通信。一个SWC可以理解为一个.c文件，那么c文件间怎么通信呢——全局变量。所以大家可以把ECU内部SWC的通信暂时先想象成全局变量，具体怎么实现的，在后续RTE章节中将做详述
2. **在片外**就通过片外总线通信（一般汽车上都是CAN Bus）

> 上图中有几个特殊的符号是指的AutoSAR接口
>
> ![在这里插入图片描述](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212222012477.png)
>
> 而它们之间蓝色的连接线成为连接器（**Connector**，也即是刚刚说的全局变量)



## 三、应用软件组件（SWC  Software Component）SWC类型

- **原子级的SWC（Atomic SWC）**

​		不可再拆分的SWC，其实之前我们列举的都是Atomic SWC，默认情况下说的SWC也是指ASWC。一个SWC是对应一个.c文件，这个c文件就是我们的最小单元，不可再分。

> 那可运行实体（runnable）不就是组成SWC的更小单元吗？确实如此，但是我们将SWC看成原子，那runnable就是其中的电子、质子和中子，它们与原子密不可分。因此将SWC看成是最小单元，runnable是其中的函数。每个SWC的功能基本都是用来实现特定的算法。

![在这里插入图片描述](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212222034714.png)

- **集合级的SWC（Composition SWC）**

​	有不可分割的SWC，就肯定有可分割的SWC。所以AutoSAR还规定了一类集合级的SWC（Composition SWC）。它们可以分为一个一个更小的Atomic SWC。就好像是一个分子由很多原子组成的概念。分子是有实际意义的，很多原子就没有实际意义（但是有些也有，比如金、银和铜等）。

| 化学概念           | AutoSAR概念     | C语言概念            |
| ------------------ | --------------- | -------------------- |
| 分子               | Composition SWC | 包含xx.c文件的文件夹 |
| 原子               | Atomic SWC      | xx.c文件             |
| 电子、中子、质子等 | runnable        | 函数                 |

还是那个例子，我们可以将功能相近或者需要整合到一处方便观看的SWC（以后Atomic SWC都简称为SWC）利用一个compositon SWC包含起来。这样，就可以方便SWC归类，这里Composition SWC有点从功能角度去看。![在这里插入图片描述](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212222105150.png)

于是，我们的文件映射也发生了一定的变化：方便大家对比，应该能很快明白composition SWC是啥了：

![在这里插入图片描述](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212222127052.png)

![在这里插入图片描述](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212222127884.png)

> **注意：** 在Vector的DaVinci中其实不会生成Composition的文件夹，其实Composition只是一个概念，是用来在配置工具上方便大家归类整理，看起来更加符合功能设定

- **特殊的SWC**

​		前面描述BSW的时候提到IO硬件抽象层（IoHwAb，BSW章节中会讲到）和复杂驱动（Cdd)，在DaVinci Developer中都是可以作为SWC进行配置和加runnable等操作的。因此，我们将其算成是特殊的SWC来看待

![在这里插入图片描述](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212222130465.png)



## 四、AutoSAR接口（Ports）和连接器（Connector）

Ports是SWC和SWC做接口（Interface）通信使用，或者SWC通过RTE和BSW做接口（Interface）通信使用。

-  **Sender Ports**发送端口![img](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212222143069.png)：提供信息

-  **Receiver Ports**接收端口![img](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212222143636.png)：接收信息

-  **Sender/Receiver Ports**发送/接收端口![img](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212222143959.png)：可在一个Port端口内提供和接收信息

-  **Server Ports**服务端口![img](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212222143842.png)：提供服务（operations)

-  **Client Ports**客户端端口![img](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212222143614.png)：使用服务（operations)

> Connector指的是**SwComponen**tType的**PortProto**types来连接建立SwComponentPrototypes之间的实际连接的SwConnector

![img](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212222229334.png)

Ports主要分为5种类型，列在下面的图中：

![在这里插入图片描述](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212222134696.png)

其中又可分类为：**R-Ports、P-Ports和PR-Ports**。值得注意的是，这里的PR-Ports是在AUTOSAR4.0以后定义。

或者又可以分为：**Send/Receiver（S/R）接口和Client/Server（C/S）**接口。



![image-20221223094342800](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212230943861.png)



![img](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212231319852.png)



需型端口可以和供型端口连接。软件组件SWC1有一个需型端口（R）和一个供型端口（P），其中需型端口与SWC2的供型端口相连，它们之间的交互关系通过连线箭头表示，由SWC2的供型端口指向SWC1的需型端口。SWC3具有一个供需端口，被认为自我相连。 由于端口仅仅定义了方向，所以AUTOSAR中用端口接口 （Port Interface）来表征**端口的属性**

![img](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212231320113.png)

软件组件SWC1具有两个端口，其中一个引用的端口接口类型为发送者-接收者（S/R）接口，另一个引用的端口接口类型为客户端-服务器（C/S）接口。从中也可以看出，对于引用发送者-接收者接口的一组端口而言，需型端口为接收者 （Receiver），供型端口为发送者（Sender）。对于引用客户端-服务器 接口的一组端口而言，需型端口为客户（Client），供型端口为服务器（Server）。

**一、S/R接口**

![在这里插入图片描述](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212222153959.png)

> **作用：** 传输数据。通过RTE传输数据，并且通过RTE管理数据的传输，避免数据出问题（例如同时调用同一数据时可能出错）
>
> 发送者-接收者接口用于**数据的传递关系**，发送者发送数据到一个或多个接收者。该类型接口中定义了一系列的数据元素（Data Element，DE），这些数据元素之间是相互独立的。如下图所示，该发送者-接收者接口SR_Interface中定义了两个数据元素，名字分别为DE_1与DE_2，并且需要为每个数据元素赋予相应的数据类型
>
> ![img](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212231327296.png)

- 一个接口可以包含多个数据，类似于通过结构体传输

- 可以传输基础数据类型（int，float等）和复杂数据类型（record，array等）

- 通信方式: 1:n 或者 n:1 

- 如果一个data element要通过总线传输， 那么它必须与一个signal对应起来

- 通信方式 - 不使用队列

  - **直接访问**

    > 适用于实时性要求高的数据，直接访问
    >
    > - RTE直接访问数据地址
    > -  初始值即为默认值

    ![image-20221223103245631](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212231032674.png)

  - **使用缓存**

    > 适用于有一致性要求的数据组
    >
    > - 在进入runnable之前RTE为数据建立副本
    > - 在runnable运行结束之后RTE把副本数据拷贝到实际数据地址
    > - 在runnable运行过程中只操作副本，实际数据不会改变

  ![image-20221223103133182](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212231031228.png)

- 通信方式-使用队列

  > **“event” (isQueued=True)**,”event“ 查询接收或等待接收，RTE从队列中读取数据，等待接收有超时处理。

  - “查询接收” 或 “等待接收”
  - RTE从队列中读取数据
  - “等待接收” 有超时处理

  ![image-20221223105749327](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212231057377.png)

  ```c
  //Read表示是一个RPort、同样也会有一个PPort，Rte_Write_xxx_xxx()
  Rte_Read_<Port>_<Data>()
  //这里Data是指的传输的数据类型，比如DoorOpen就是：
  SWC_DoorOpen = Rte_Read_Door_DoorOpen();
  ```

-  对于S/R通信模式，分为显示（Explicit）和隐式（Implicit）两种模式。当多个运行实体需要读取相同的数据时，若能在运行实体运行之前先把数据读到缓存中，在运行实体运行结束后再把数据写出去，则可以改善运行效率，这就是**隐式模式。**

  ![img](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212231332721.png)

**二、C/S接口**

![在这里插入图片描述](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212222214824.png)

> **作用：** 提供操作。就是Server提供函数供Client调用
>
> 客户端-服务器接口用于操作（Operation，OP），即函数调用关系，**服务器是操作的提供者**，多个客户端可以调用同一个操作，但同一个客户端不能调用多个操作。客户端-服务器接口定义了一系列操作 （Operation），即函数，它（们）由引用该接口的供型端口所在的软件组（服务器）件来实现，并提供给引用该接口的需型端口所在的软件组件调用。如下图所示，该客户端-服务器接口CS_Interface中定义了两个操作OP_1 与OP_2，对于每一个操作需要定义相关参数及其方向，即函数的形参，需要注意的是，每个端口只能引用一种接口类型，并且引用相同端口接口类型的端口才可以进行交互。
>
> ![img](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212231327902.png)

- 可以同步和异步。同步就是直接调用，相当于函数直接插入上下文运行；异步的话需要等待，相当于让函数在另一个线程中运行，运行完了再返回，原上下文依然运行

  ![img](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212231324726.png)

- 一个接口可以提供多个操作，就是一个接口可以包含很多函数

- ECU内部和跨ECU都可以调用，跨ECU也是通过外部总线

- 通信方式: 1:1 或 n:1 （与S/R对应）

  ```c
  Rte_Call_<Port>_<Function>()
  //这里的Call是指的调用的函数，比如调用State()就是
  Rte_Call_Door_State();
  ```





# Runnable entities (简称Runnables)

Runnable就是SWC中的函数，而在AutoSAR架构在被DaVinci软件生成的时候，Runnable是空函数，需要手动添加代码来实现其实际的功能。
Runnable可以被触发，比如被定时器触发、被操作调用触发或者被接受数据触发等。

![在这里插入图片描述](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212222231713.png)

这里的函数就是我们前面提到的**Send**接口，发送的就是DoorOpen这个数据，由RTE进行管理。然而由于这里的这个SWCn.c文件中并未包含BSW中的.h文件，通过这个方式将AppL和BSW隔离开。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190720113021314.png)

> Runnable是需要OS中的Task做载体的。runnable是函数，但是c文件中光有一个函数那没用，必须要调用该函数才能起作用，就必须要有操作系统中的任务来执行这个函数。类比于Linux中的线程就是Task，这里的Runnable更多的像内核中的**threadfn**，或者说是Java中Runnable，需要载体，另外在AppL中没有Task这个概念。





**举个例子：**

从传感器到应用程序的过程:

![image-20221223094615901](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212230946951.png)



>  **代码什么样？**



**1.Runnable Entity(可运行实体 ）**

Runnable是主要用来封装SWC中的功能的。是由C语言函数实现的。一个SWC中需要至少要包含一个Runnable。简单举个例子：

```text
CheckStatusRunnable()
{
/* 判断是否完成 */
    if(!finished)
    {
/* 如果未完成，就返回不OK */
        return E_NOT_OK;
    }
    return E_OK； //如果完成，返回OK
}
```



Runnable 简单分为两类：

**Category 1**：No WaitPoint （在有限的时间内运行至结束，不能等待）。

**Category 2**：With a WaitPoint at least.（至少包含一个WaitPoint，运行过程中可以等待）



**怎么在Runnable中设置WaitPoint？通过直接调用对应RTE API实现。**

**Rte_Receive() : 用于等待接收数据；**

**Rte_Feedback() : 用于等待数据发送完成；**

- Rte_Invalidate_<p>_<d>()，表示sensor发送的数据无效，接收方feedback对无效值的处理

**Rte_SwitchAck() : 用于等待模式切换操作；**

**Rte_Result() : 用于等待异步服务器调用的结果。**





**2. Task（任务）**

是操作系统（OS）管理的最小可调度单元。操作系统决定何时在ECU的CPU上运行哪个任务。在OS启动后，所有的Task都处于默认状态：挂起状态（Suspended）。Task被激活（Activated）后进入准备状态（Ready）。Ready的task将会按照优先级（Priority）的高低依次运行（Running）。

在RTE的代码中：

```text
TASK(TSK_Task1)
{
    ...
    Runnable1();
    Runnable2();
    CheckStatusRunnable();
    Runnable3();
    ...
  }
}
TASK(TSK_Task2)
{
  ...
}
```

**当TSK_Task1被激活并运行后，map到它的Runnable也会按map的顺序依次执行。**





**3.运行实体的RTE事件（RTE Event）**

每个运行实体都会被赋予一个RTE事件（Trigger Event），即RTE 事件（RTE Event），这个事件可以引发这个运行实体的执行。对于 RTE事件可以细分为很多种类，较常用的RTE事件有以下几种：

- 周期性（Periodic）事件，即Timing Event；
- 数据接收事件（Data-received Event）；
-  客户端调用服务器事件（Server-call Event）。
