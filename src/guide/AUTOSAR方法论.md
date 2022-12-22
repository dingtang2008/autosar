# AUTOSAR方法论 (methodology)

## 一、ECUEX简介

什么是ECUEX文件呢？开始提到**ECU提取文件**（全称是**ECU Extract of System Description**），简单说就是OEM和TIER1交接的文件。该文件由OEM设计整车时生成，并根据不同的ECU提取出对应的ECUEX文件交接给TIER1，TIER1拿到文件后便可以根据上面的信息来设计和开发ECU。ECUEX文件是arxml文件，但是如果只做通信矩阵这些内容，DBC(**Database Can**)这类文件也可以胜任（不过随着时代的进步，以后还是arxml）。

![在这里插入图片描述](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212222330011.png)

要可以包含以下内容（也可以只包含其中一部分）：

- **通信矩阵：** 比如CAN总线包含的信息，像CAN ID号、signals、扩展帧还是普通帧和波特率之类的信息
- **SWCs、Ports等：** SWC以及内部的runnable都可以在ECUEX文件中给出；还包含其Ports；还有SWC之间的连接关系（Connecters）
- **数据映射（Data Mapping）：** 将总线的信号（Network Signals）映射到SWCs中





ECUEX文件可以很简单（简单到只有通信矩阵），也可以很复杂（复杂到连一部分代码都要自己写）。

**某些OEM和TIER1的分工，不绝对，未来OEM会负责更多的事务：**

| 名称               | 解释                                                     | OEM    | TIER1  |
  | ------------------ | -------------------------------------------------------- | ------ | ------ |
  | Service Components | 为SWCs提供实际使用的BSW服务的接口（需要在BSW中配置过了） | 不负责 | 负责   |
  | Service Mapping    | 连接SWCs和Service Components                             | 不负责 | 负责   |
  | Atomics            | 功能的具体实现                                           | 不负责 | 负责   |
  | Compositions       | 每个SWC上需要哪些Port、连接器之类的                      | 不负责 | 负责   |
  | Data Mapping       | 连接Network Signals到SWCs中                              | 不负责 | 负责   |
  | ECU Composition    | 就是需要哪些SWC                                          | 不负责 | 负责   |
  | Communication      | 就是上面说的通信矩阵                                     | 负责   | 不负责 |



## 二、AutoSAR开发流程

![image-20221222234129917](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212222341969.png)
