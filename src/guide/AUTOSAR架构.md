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



## AUTOSAR架构分层

分层架构是实现软硬件分离的关键，使汽车系统软件开发者摆脱了之前ECU软件开发与验证时对硬件系统的依赖,在AUTOSAR分层架构中，汽车嵌入式系统软件自上而下分别为：

- 应用软件层（Application Software ,**ASW**）
- 运行时环境 （Runtime Environment，**RTE**）
- 基础软件层（Basic Software Layer， **BSW**)
- 微控制器（Microcontroller）

![image-20221220172941975](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212201729014.png)



### 1、基础软件层（Base Software Layer）

- 进一步，BSW 基础软件层（Basic Software Layer，BSW）又可分为四层:
  - 微控制器抽象层（Microcontroller Abstraction Layer，**MCAL**）
  - ECU抽象层（**ECU** Abstraction Layer）
  - 服务层（**Services** Layer）
  - 复杂驱动 （Complex Drivers）


![image-20221220171927299](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212201719333.png)

- 基础软件层被进一步划分为功能组（**functional groups**）。服务层**（Services Layer）** 分为系统服务、内存服务和通信服务等。

![image-20221220180442655](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212201804696.png)





#### 1.1 微控制器抽象层（Microcontroller Abstraction Layer）
微控制器抽象层是基本软件中最低的软件层。它包含内部**驱动程序**，这是一种可以直接访问µC和内部外设的软件模块。微控制器抽象层包括
  ![image-20221220180419618](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212201804655.png)


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

![image-20221220181113543](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212201811582.png)



#### 1.2  ECU抽象层（ECU Abstraction Layer）

ECU抽象层（ECU Abstraction Layer）包括板载设备抽象 （Onboard Devices Abstraction）、存储器硬件抽象 （Memory Hardware Abstraction）、通信硬件抽象 （Communication Hardware Abstraction）和I/O硬件抽象 （Input/Output Hardware Abstraction）。

​    该层将ECU结构进行了抽象，负责提供统一的访问接口，该层与ECU平台相关，但与微控制器无关。
