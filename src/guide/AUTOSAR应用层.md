![image-20221222163858277](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212221638322.png)

## 一、AppL的组成

AppL中最重要的就是SWC了，而SWC与其他SWC通信需要接口，每个SWC中又由runnable组成，所以AppL主要的组成就分下面三部分：

1. 应用软件组件（SWC）
2. AutoSAR接口（Ports）和连接器（Connector）
3. 可运行实体（Runnable）