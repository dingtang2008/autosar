

# AUTOSAR文档如何阅读

从autosar.org官网可以看到，autosar有这些文档

![image-20221218131713772](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212181317839.png)



基本上一年一个版本，目前已经release了R22版本，22年11月份。

![image-20221220165144730](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212201651762.png)

## Classic Platform

**AUTOSAR Classic Platform**主要运行在MCU上的三个软件层之间：应用程序，运行时环境（RTE）和基本软件（BSW）。

应用软件层主要与硬件无关。
软件组件之间的通信以及通过RTE访问BSW。
RTE代表应用程序的完整接口。
BSW分为三个主要层和复杂的驱动程序：Services, ECU (Electronic Control Unit) abstraction和microcontroller abstraction。
服务进一步分为代表系统，内存和通信服务基础架构的功能组。
