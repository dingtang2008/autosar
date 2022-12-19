# AUTOSAR的简介

![AUTOSAR](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212150004306.svg)是汽车和软件行业领先公司的全球合作联盟，为智能移动开发和建立标准化的软件框架以及开放的E/E系统架构。考虑到目前和*未来市场中不同的汽车E/E架构*(Electrical/Electronic Architecture)，他们制定了一套专门用于汽车的开放性的框架和行业标准，它将用作管理将来的应用程序和标准软件模块中功能的基本基础结构。AUTOSAR的是**AUT**omotive **O**pen **S**ystem **AR**chitecture的缩写，是一种软件架构，因此AUTOSAR有两种含义：

1. 代表**AUTOSAR联盟**
2. 代表**AUTOSAR软件架构**。

![图片](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212181208858.jpeg)

<h5 align="center">AUTOSAR</h5>

## 一、AUTOSAR成员

[AutoSAR官网的成员的介绍界面](https://www.autosar.org/about/partners/)，目前有**7类**合作伙伴(最近新增了premium plus)

- 核心合作伙伴（创始成员9个无法申请），战略合作伙伴一个**电装**
- 高级合作伙伴 +
- 高级合作伙伴
- 开发合作伙伴
- 关联合作伙伴
- 参与者
- 订阅者

![img](https://www.autosar.org/fileadmin/_processed_/4/5/csm_Autosar_Partner_Types_51abd0ae99.jpg)

<h5 align="center">AUTOSAR会员类型</h5>

## 二、合作伙伴

目前已经有超过300+AUTOSAR合作伙伴。

![image-20221215000931440](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212150009510.png)

<h5 align="center">AUTOSAR合作伙伴</h5>



## 三、成员发展

> 西门子VDO原本也是核心成员，被Continental 收购，因此西门子VDO不再是AUTOSAR的核心成员

![img](https://www.autosar.org/fileadmin/_processed_/5/6/csm_csm_partner_history_e2ab579698_d648bcfbe9.png)

<h5 align="center">合作伙伴发展历史</h5>

![image-20221218153811580](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212181538756.png)

<h5 align="center">AUTOSAR合作伙伴的遍布全球</h5>

## 四、AUTOSAR的诞生

基于以上思想，AUTSOAR 软件架构分为

- 应用层AppL(Application Layer)
- 运行时环境层RTE(Runtime Environment)
- 基础软件层BSWL(Basic Software Layer)

应用层侧重于应用软件的开发,由软件组件(SWC，Sotware Component)组成,各个软件组件内部可以包含一个或多个运行实体(Runnable Entity),软件组件之间通过 Port端口形成逻辑连接。运行时环境层为软件组件之间及软件组件与基础软件之间提供虚拟总线功能VFB(Virtual Function Bus),即软件组件与其他软件组件或基础软件的数据交互需要通过运行环境层提供的标准软件接口实现。运行环境层与微控制器之间为基础软件层。这种分层架构优势在于:一方面,OEM可以专注于开发特定的、有竞争力的应用层软件(在运行环境层之上);另一方面,它使 OEM 所不关心的基础软件层(在运行环境层之下)得到OEM:帮车/标准化。





## 五、AUTOSAR带来了什么好处

- 对于**OEM**车厂

![image-20221218205705166](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212182057233.png)

- 对于**供应商**

![image-20221218205714959](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212182057027.png)

- 对于**工具供应商**

![image-20221219105650964](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212191056028.png)

- 对于**新入市场者**

![image-20221219110253540](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212191102603.png)

##### 

