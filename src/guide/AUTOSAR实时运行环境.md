



![在这里插入图片描述](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212222237710.png)



## 一、什么是RTE

RTE的作用有点像Binder的**ServiceManger**，或者说DNS（就是上个世界那种要先打电话到接线员那里，然后通过接线员转接电话线到目的地），其作用就是将一个SWC的信息通过RTE连接到其他SWC或者BSW上。且RTE具有管理这些信息的功能，比如接收的SWC正忙（您所拨打的用户正忙），那么RTE负责让发送信息的SWC等待，或者做其他处理；RTE还能触发SWC，就像是这时接收的SWC在睡觉，这时发送的SWC发信息来了，那么RTE就要把接收的SWC叫醒起床。一句话概括就是RTE提供了SWC的运行环境。

## 二、RTE的作用

- 提供 **跨ECU / ECU内部** 的通信管理。
- 提供 对runnable的管理功能（触发、唤醒等，简单说就是runnable需要映射到Task上运行嘛，而这个映射就是通过RTE具体实现的）
- 之前我们不是提到了VFB（虚拟功能总线），RTE就是VFB的具体实现
- 在Vector的工具链中，RTE是自动生成的

下面这张图将其再做细化，就能很清楚的看出其关联关系了。这里的RTE就是统一的管理，具体那些连接时怎么连的，我们是不需要在RTE中关心的（因为AppL中配好，RTE就自动生成嘛）。

![在这里插入图片描述](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212222252983.png)



## 三、RTE主要功能点

- **通过RTE给runnable提供触发事件。** 之前说过了runnable是可以被触发的，就是需要通过RTE来实现这个触发和调用runnable
- **通过RTE给runnable提供所需资源。** 就是之前说的接口通信，将runnable需要的一些资源通过接口传输给它
- **将BSW和SWC做隔绝。** 因此OS和runnables也被隔绝了，runnable的运行条件由RTE提供，不能由OS直接提供

![在这里插入图片描述](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212222258357.png)



## Runnables的触发条件

| **Abbreviation** | **Name**                                                   | 触发条件                                                     |
| ---------------- | ---------------------------------------------------------- | ------------------------------------------------------------ |
| T                | TimingEvent                                                | 定时器事件：给一个周期定时器，时间到了就触发                 |
| BG               | BackgroundEvent                                            |                                                              |
| DR               | DataReceivedEvent (S/R Communication only)                 | 接收数据事件（S/R）：Receiver Port 一旦收到数据，就触发      |
| DRE              | DataReceiveErrorEvent (S/R Communication only)             | 接收数据错误事件（S/R）                                      |
| DSC              | DataSendCompletedEvent(explicit S/R Communication only)    | 数据发送完成事件（S/R）：Send Port 发送完成，就触发          |
| DWC              | DataWriteCompletedEvent (implicit S/R Communication only)  | 数据写入完成事件（S/R）：Send Port 发送完成，就触发          |
| OI               | OperationInvokedEvent (C/S Communication only)             | 操作调用事件（C/S）：当调用到了该函数的时候                  |
| ASCR             | AsynchronousServerCallReturnsEvent(C/S communication only) | 异步服务返回事件（C/S）：之前说过C/S可以在异步下运行，就是说当我调用一个Server函数，但是我是异步调用的。那么该被掉函数作为一个线程和当前的运行程序并行运行，当被调函数运行结束返回（Return）的时候，这时触发异步服务返回事件 |
| MS               | SwcModeSwitchEvent                                         | 模式切换事件                                                 |
| MSA              | ModeSwitchedAckEvent                                       | 模式切换事件                                                 |
| MME              | SwcModeManagerErrorEvent                                   |                                                              |
| ETO              | ExternalTriggerOccurredEvent                               |                                                              |
| ITO              | InternalTriggerOccurredEvent                               |                                                              |
| I                | InitEvent                                                  | 初始化事件：初始化自动触发                                   |
| THE              | TransformerHardErrorEvent                                  |                                                              |



















# AUTOSAR的接口



![image-20221222231421708](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212222314767.png)

AUTOSAR中定义了三种接口，`AUTOSAR Interface`, `Standardized Interface` 以及 `Standardized AUTOSAR Inerface`. 要了解这三种接口，需要首先了解什么是"Standardized"的Interface，以及什么是"AUTOSAR"的Interface.

**Standardaized** 表示的是，这个接口是被事先标准化定义好的, 需要注意的是这里的"标准化定义"，指得就是被AUTOSAR这个标准所定义。用户在使用这个接口的时候，不可以改变接口的内容。所谓"接口"，其实就是一个API函数. AUTOSAR标准中的软件模块被事先定义好，需要向其它模块提供哪些API函数, **这些API函数的输入输出变量的个数，类型以及返回值的类型都会被事先定义好，不能改变**。在开发时需要做的，就是开发API中的内容。

**AUTOSAR** 的接口指的**RTE提供的接口**。RTE向所有的SWC，以及IoHwAb和Complex Drivers模块，提供AUTOSAR 接口，也就是说，这些模块都会连接在RTE上面。当某两个这类模块之间互相收发数据或者调用内部函数时，RTE会帮助它们来做这些。

理解了Standardized Interface 和 AUTOSAR Interface, 那么 **Standardized AUTOSAR** Interface 就容易理解了。指的是，被AUTOSAR标准**提前定义好的**，并且是**由RTE提供**的接口。

下面这个表格是关于这三个接口的总结:

| 是否被AUTOSAR标准提前定义好?       | 是否属于RTE提供的接口? | 模块是否连接在RTE上?                     |
| ---------------------------------- | ---------------------- | ---------------------------------------- |
| **Standardized** Interface         | 是                     | 否，模块之间的API调用不需要通过RTE的帮助 |
| AUTOSAR Interface                  | 否，可以任意改变       | 是                                       |
| **Standardized** AUTOSAR Interface | 是                     | 是                                       |

> OS和COM是唯一的两个标准接口允许直接和RTE相连的。因为RTE的很多功能是需要基于这两个模块来实现的。



还是回到之前的案例，如下图

![在这里插入图片描述](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212222315979.png)

上图将所有的接口以及其分布的位置都详细的标识了出来，还是用的原来的那张ECU的图添加，结合上面的描述和上图：

**AutoSAR接口**

- **一句话概括：** 之前说的S/R和C/S接口就是AutoSAR接口
- **特征：** 接口函数名可变，例如之前说过的`Std_ReturnType Rte_Read_<port>_<data> (<DataType> *data)`这中形式的S/R函数，其中的`<port> <data>`就是用户自己配置的名字，因此，这些接口的函数名都是可以改变的，但大体的形式是不变的。
- **位置：** SWC<>RTE、RTE<>CDD、RTE<>ECU AB(这里提一句，ECU AB之前没有讲到，其实很多的传感器、执行器都放在这里，是ECU的抽象，也是可以看作是SWC的，IoHwAb就在这里面)。说明白一点，就是只要能看成是SWC处理的，就是AutoSAR接口

**标准接口**

- **一句话概括：** 就是AutoSAR规定的C语言API
- **特征：** 接口函数名是固定不变的，是AutoSAR规定好的。比如：`Com_SendSignal() WaitEvent()`这类都是API函数名，可以有上层调用，但是一般是使用工具配置生成的，做上层应用的一般是不用关心其具体实现的
- **位置：** 第一张图中棕色的就是标准接口，说白了就是对函数API的调用。

需要特殊说明一点的是：下图中两个红圈中的箭头，OS和COM是唯一的两个标准接口允许直接和RTE相连的。因为RTE的很多功能是需要基于这两个模块来实现的

**标准AutoSAR接口**

- **一句话概括：** 就是AutoSAR接口，不过名称是由AutoSAR官方规定不能修改
- **特征：** 就是标准接口和AutoSAR接口的特征它都有一部分。首先是和AutoSAR接口一样，提供的是C/S、S/R接口；然后又和标准接口一样，函数名是不可变的。说白了就是官方规定好的C/S、S/R接口，咱们就当成是AutoSAR接口就行了，函数名字什么不用管它
- **位置：** RTE<>Services，就这么一个地方
