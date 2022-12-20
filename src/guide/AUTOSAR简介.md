# AUTOSAR的简介

![图片](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212181208858.jpeg)

<h5 align="center">AUTOSAR</h5>

![AUTOSAR](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212150004306.svg)是汽车和软件行业领先公司的全球合作联盟，为智能移动开发和建立标准化的软件框架以及开放的E/E系统架构。考虑到目前和*未来市场中不同的汽车E/E架构*(Electrical/Electronic Architecture)，他们制定了一套专门用于汽车的开放性的框架和行业标准，它将用作管理将来的应用程序和标准软件模块中功能的基本基础结构。AUTOSAR的是**AUT**omotive **O**pen **S**ystem **AR**chitecture的缩写，是一种软件架构，因此AUTOSAR有两种含义：

1. 代表**AUTOSAR联盟**

2. 代表**AUTOSAR软件架构**。

   

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

![image-20221220195204392](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212201952478.png)

<h5 align="center">AUTOSAR合作伙伴</h5>



## 三、成员发展

> 西门子VDO原本也是核心成员，被Continental 收购，因此西门子VDO不再是AUTOSAR的核心成员

![img](https://www.autosar.org/fileadmin/_processed_/5/6/csm_csm_partner_history_e2ab579698_d648bcfbe9.png)

<h5 align="center">合作伙伴发展历史</h5>

![image-20221218153811580](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212181538756.png)

<h5 align="center">AUTOSAR合作伙伴的遍布全球</h5>



## 四、AUTOSAR的组织

- AUTOSAR标准主要是由**AUTOSAR Working Group**组织制作的

![image-20221220150420358](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212201504421.png)

- AUTOSAR还有一个用户组，用户组是变化的，当前主要有三个用户组：

  - **UG-CN China，UG-CN的愿景是为中国市场启用AUTOSAR。**

    - 为了实现此目标，用户组在AUTOSAR演示程序项目上工作，以提供用户指南“如何从AUTOSAR开始”和演示程序的启动配置。

  - **UG-NA North America，UG-NA的愿景是增强北美用户在AUTOSAR方面的技能，以充分利用AUTOSAR带来的汽车EE体系结构开发的优势。**

    - 为实现这一愿景，他们提供了一个协作环境，以促进AUTOSAR在北美地区的使用。
    - 开发关键文档以帮助理解AUTOSAR标准，并提供示例和配置以解决特定的用例。

  - **UG-IE Improved Exploitation，UG-IE代表了更好地利用AUTOSAR工业标准。**

    - 他们的任务是分享AUTOSAR的利用和开发经验。其他任务包括为战略方向准备提案，以提高AUTOSAR的可用性以及节省更多的精力。
    - UG-IE的总结结果创建了演示文稿和技术论文，对AUTOSAR战略，技术工作组和用户产生了推动作用。

    

    



![image-20221220154850123](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212201548167.png)

- **AUTOSAR软件框架**，AUTOSAR分为CP和AP和合作平台

![image-20221220153214810](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212201532865.png)



| 指标         | CP             | AP            |
| ------------ | -------------- | ------------- |
| 开发工具     | C              | C++           |
| 开源程度     | 非开源         | 开源          |
| 适用环境     | 传统ECU、MCU   | 自动驾驶、V2X |
| 实时方式     | 硬实时         | 软实时        |
| 通信方式     | CAN、LIN       | 以太网        |
| 操作系统     | OSEK-OS based  | POSIX         |
| 升级方式     | 固定，不可升级 | SOA           |
| 功能安全等级 | ASIL D         | ASIL B以上    |

<h5 align="center">图1：AUTOSAR CP和AP对比</h5>

- **AUTOSAR交付内容**

  从“Foundation”出发的，扩展出Classic Platform（简称CP）和Adaptive Platform（简称AP）两大平台，继而定义各种接口和测试等。

  - CP交付了规范文档
  - AP提供示例代码和文档
  - 白色部分属于还在扩展中的部分标准

![image-20221220160634363](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212201606424.png)

- Foundation(FO)主要作用是确保不同AUTOSAR标准的兼容性，因此包含了所有常见的Artifact和协议，例如

  ![image-20221220161033000](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212201610063.png)

## 五、AUTOSAR带来了什么好处

- 对于**OEM**车厂

![image-20221218205705166](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212182057233.png)

- 对于**供应商**

![image-20221218205714959](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212182057027.png)

![image-20221220161548667](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212201615733.png)

- 对于**工具供应商**

![image-20221219105650964](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212191056028.png)

- 对于**新入市场者**

![image-20221219110253540](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212191102603.png)









