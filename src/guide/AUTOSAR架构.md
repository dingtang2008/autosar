# AUTOSAR架构
AUTOSAR总的思想是，`Cooperate on standards – Compete on implementation`，**标准上合作，实现上竞争。**

意思就是**汽车行业的整车厂和供应商共同合作开发一套汽车电子系统的软件开发标准，这样大家就可以专注于功能的开发，而无需顾虑目标硬件平台。**

- 将汽车系统的基础软件标准化为一个跨OEM的 **标准栈**

- **集成**不同供应商生产的功能模块

- **适用**于不同的车辆及不同的车型

AUTOSAR的计划目标主要有三个：

- 规范分布式开发流程中的**交换格式**
- 为应用程序的开发提供**方法论**
- 制定各种**应用接口规范**

![image-20221220164436028](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212201644103.png)

<h5 align="center">AUTOSAR的使用</h5>

## AUTOSAR架构分层

AUTOSAR的应用范围：AUTOSAR专用于汽车ECU。此类ECU具有以下属性：

- 与硬件（传感器和执行器）强交互
- 与CAN、LIN、FlexRay或以太网等车辆网络的连接，
- 具有有限计算能力和内存资源的微控制器（通常为16或32位）（与企业解决方案相比）
-  实时系统和从内部或外部闪存执行程序。







分层架构是实现软硬件分离的关键，使汽车系统软件开发者摆脱了之前ECU软件开发与验证时对硬件系统的依赖,在AUTOSAR分层架构中，汽车嵌入式系统软件自上而下分别为：

- 基础软件层（Basic Software Layer， **BSW**)
- 应用软件层（Application Software ,**ASW**）
- 运行时环境 （Runtime Environment，**RTE**）
- 微控制器（Microcontroller）

![image-20221220172941975](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212201729014.png)

<h5 align="center">AUTOSAR分层示意图</h5>

### 1、基础软件层（Base Software Layer）

- 进一步，BSW 基础软件层（Basic Software Layer，BSW）又可分为四层:
  1. 微控制器抽象层（Microcontroller Abstraction Layer，**MCAL**）
  2. ECU抽象层（**ECU** Abstraction Layer）
  3. 服务层（**Services** Layer）
  4. 复杂驱动 （Complex Device Drivers  ，**CDD**）



![image-20221220171927299](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212201719333.png)

<h5 align="center">基础软件层详细划分</h5>

- 基础软件层被进一步划分为功能组（**functional groups**）。服务层**（Services Layer）** 分为系统服务、内存服务和通信服务等。

![image-20221220180442655](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212201804696.png)

<h5 align="center">基础软件功能分组</h5>

从上图可以看到，BSW这一层的划分有点乱，既有纵向的，也有横向的，CDD可以认为是纵向的独立的一个功能组，这些跨越多个层级的都是一些比较特殊的，比如左侧的系统服务跨越多个层级，并且包含了OS(AUTOSAR OS后面描述)；然后还有一个I/O硬件抽象。每个功能组在纵向上都是一个分类，但这并不是说每个模块/功能组只能在自己所属纵向上使用。比如SPI底层驱动可能划分在Communication Drivers里面。但是该模块的调用路径很可能是通过RTE → I/O Hardware Abstraction → SPI。但是像**CAN**这种外设，它就是通过RTE → Communication Services → Communication Hardware Abstraction → Communication Drivers/CAN这条线来使用的。

#### 1.1 微控制器抽象层（Microcontroller Abstraction Layer）
微控制器抽象层是基本软件中最低的软件层。它包含内部**驱动程序**，这是一种可以直接访问µC和内部外设的软件模块。

![image-20221221143024193](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212211430245.png)

<h5 align="center">微控制器抽象层</h5>

**任务：**

让MCAL层的上层软件独立于/不依赖微控制器。

**特性：**：

- 实现：依赖于µC的实现

- 接口：标准化和µC独立

> **举个例子：**
>
> 例如我们现在有一个芯片A，基本开发完成了，但是为了cost down，，要求换个芯片吧（叫芯片B），芯片B不但便宜，还Pin2Pin兼容。这时候做应用及上面服务层的同事一片叫好（反正没他们啥事，吃瓜群众）。做MCAL的人就苦逼了，他们得重新针对新的芯片B重新弄一遍。这就是上面不依赖于芯片，有MCAL搞定。

微控制器抽象层包括：

![image-20221220180419618](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212201804655.png)

<h5 align="center">微控制器抽象层驱动分组</h5>

![image-20221220181113543](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212201811582.png)

<h5 align="center">微控制器层详细划分</h5>

如果更详细一点的划分如上图


- **微控制器驱动**（Microcontroller Drivers）
  - 内部外设的驱动程序（如看门狗、通用计时器）功能
  - 具有直接访问µC的函数（如核心测试）

- **存储器驱动** （Memory Drivers）
  - 芯片上存储设备（例如内部Flash、内部EEPROM)和内存映射的外部内存设备（例如外部闪存）的驱动程序

- **加密驱动** 

  -  如SHE(Secure Hardware Extension)或HSM(Hardware Secure Module)等芯片上加密设备的驱动程序
- **无线通信**（Wireless Communication Drivers）

  - 无线网络系统的驱动（V2X、车内无线网络系统和非车载ECU通信系统）

- **通信驱动**（Communication Drivers）

  - 车载ECU(如SPI)和车辆通信(如CAN)
  - OSI网络分层结构的数据链路层的一部分
  - SPIHandlerDriver
    - **SPIHandlerDriver**允许并行访问一个或多个SPI总线
    - 为了抽象专用于芯片选择的SPI微控制器引脚的所有特征，这些特征应由**SPIHandlerDriver**直接处理。这意味着这些引脚在DIO Driver中不可用。
    ![image-20221220182440436](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212201824464.png)

- **I/O驱动** （I/O Drivers）
- 模拟和数字I/O的驱动程序（如ADC、PWM、DIO)





#### 1.2  ECU抽象层（ECU Abstraction Layer）

ECU抽象层与微控制器抽象层的驱动程序接口。它还包含外部设备的驱动程序。它提供了一个API 用于访问外围设备和设备，无论其位置（µC内部/外部）以及与µC的连接（端口引脚、接口类型）

**任务：**

使更高的软件层独立于ECU硬件布局

**特性：**

实现：µC独立，依赖于ECU硬件

上层接口：独立与µC和ECU硬件

![image-20221221143342316](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212211433352.png)

ECU抽象层（ECU Abstraction Layer）包括

- 板载设备抽象 （Onboard Devices Abstraction）
- 存储器硬件抽象 （Memory Hardware Abstraction）
- 通信硬件抽象 （Communication Hardware Abstraction）
- I/O硬件抽象 （Input/Output Hardware Abstraction）。

![image-20221221181332552](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212211813608.png)

ECU抽象层**有点类似于Android平台的AOSP 标准化的HAL层**，ECU抽象层是MCAL层的接口，这一层里面有很多名为**Xxx_If**的模块，与MCAL层相应模块对应。实际上这一层也包含驱动程序，但是是针对外部设备的驱动，而前面提到的MCAL是针对微控制器内部外设的。

> 举个例子:
>
> 由于MCU的资源有限，有些时候我们需要使用外扩Flash，通常这种外扩Flash是通过SPI这种端口连接的。我们知道芯片内部自带的Flash是由MCAL里面的Fls模块负责的，那现在这个外扩Flash就自能自己实现.

![image-20221221180943302](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212211809350.png)



#### 1.3 服务层（**Services** Layer）

服务层（Services Layer）可分为系统服务（System Services）、存储器服务 （Memory Services）以及通信服务（Communication Services）**三大部分**。提供包括网络通信管理、存储管理、ECU模式管理和实时操作系统 （Real Time Operating System，RTOS）等服务。除了操作系统外，服务层的软件模块都是与ECU平台无关的。

![image-20221222154352692](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212221543730.png)

![image-20221222154253701](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212221542781.png)

服务层是基础软件的最高层，它提供了：

- 操作系统功能
- 车辆网络通信管理服务
- 内存服务（NVRAM管理）
- 诊断服务（包括UDS通信，内存错误和故障处理）
- ECU状态管理，模式管理
- 逻辑和程序时序流监控（Wdg管理）



**任务：**

给应用层，RTE，BSW模块提供基础服务。

**特性：**

实现：除了OS部分功能外,不依赖于µC和ECU

接口：µC和ECU硬件独立

>**注意：**
>
>对I/O信号的访问是由ECU抽象层实现的。上面提到服务层应用层，RTE提供服务比较号理解。容易忽略的是也对BSW模块提供服务，其实也很好理解，比如其他BSW模块可能不可避免的需要使用OS服务。这又涉及到前面提到过的调用关系了。总的来说大的原则是从上至下调用。但横向互相调用也是可以的。只有下面调用/通知上面这种情况，AUTOSAR使用callback机制。



#### 1.4 复杂驱动层（**Complex Drivers Layer** ）

![image-20221222154734224](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212221547260.png)

![image-20221222155009788](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212221550840.png)

如图所示，复杂驱动层从硬件直接跨越到RTE层。CDD为集成特殊功能提供了可能性。

**任务：**

- 那些没有在AUTOSAR里面规定的外设驱动。
- 对时序约束很高的驱动。
- 或者用于迁移集成等。

**特性：**

实现：可能是依赖于应用程序、µC和ECU的硬件的

上层接口：可能是依赖于应用程序、µC和ECU的硬件的

>  注意：
>
> CDD虽然名字叫驱动，但它其实也可以是应用程序。例如vector的实现就是将CDD归类为SWC 与ECU硬件及MCU相关。



### 2、运行时环境层（Runtime Environment Layer）

![image-20221222155420330](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212221554367.png)

![image-20221222155557873](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212221555910.png)

RTE是为应用软件提供通信服务的。这些AUTOSAR软件组件之间/软件组件与服务之间的通信都由RTE来实现。这里说的应用软件包含AUTOSAR软件组件/传感器/执行器组件等。在RTE以上的软件架构风格由下面这种“层”的概念变为“软件组件”的风格。

**任务**

针对ECU进行映射以达到AUTOSAR组件完全独立/不依赖于ECU。

**属性**

实现：ECU和特定应用（为每个ECU单独生成）

接口：完全独立于ECU
