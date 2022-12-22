

# AUTOSAR文档如何阅读

## 1、文档查询

从autosar.org 官网可以下载和查询文档：

![image-20221218131713772](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212181317839.png)

<h5 align="center">AUTOSAR官网</h5>



选中classic可以看到有的版本，通过search按钮可以查询对应的文档。

![image-20221222103458870](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212221034945.png)



基本上一年一个版本，目前已经release了R22版本，22年11月份。

![image-20221220165144730](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212201651762.png)







由于官网的维护和改版，和之前的版本有了较大的变化，没有办法按照功能组去下载对应的文档了。





![img](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212221039804.png)

## 2、文档类型





文档目前官网处于R22发布重新维护中，当前文档服务无法提供，文档也无法下载，需要下载的我这边可以提供。

![image-20221222100214908](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212221002973.png)

<h5 align="center">AUTOSAR文档目录</h5>

可以看到从文件命名的格式来看，都是AUTOSAR开头，以AUTOSAR_XXX_YYY 等结尾，XXX主要分为如下几个大类：

| 简写         | 详细含义                            | 解释                                       |
| ------------ | ----------------------------------- | ------------------------------------------ |
| EXP          | Explaination                        | 解释说明性的文档，**优先阅读**             |
| EXP_FCDesign | FUNCTIONAL CLUSTER DESIGN           | 示例代码的设计文档，帮助更好地理解 FC 模块 |
| RS           | Requirement Specification           | 详细描述需求规范                           |
| SRS          | Softeware Requirement Specification | 所有软件模块需求规范                       |
| SWS          | Softeware Specification             | 软件模块设计和实现的规范                   |
| TPS          | Template Specification              | 模板详细介绍                               |
| TR           | Technical Report                    | 技术规范详细介绍                           |
| MOD          | Model                               | 建模                                       |
| MMOD         | Meta Model                          | 元模型                                     |

>  文档下载列表中带有 `GENERAL` 的为 High-level 的一般性文档，应该优先阅读。

下面详细解释一下各项简写的意思：

- **MMOD：**Meta Model，介绍AUTOSAR的元模型

  > **元模型的本质是沟通工具，是模型的模型**
  >
  > 举个例子：一个具体的流程图，比如应用启动流程、消息发送流程等都是**模型**，而让不同的人看到模型都能理解其中的含义就是元模型的功劳了，具体来说就是方框代表什么、菱形代表什么，更直白点就是你画图的时候工具栏上的工具条。
  >
  > 没错，我们常说的UML，就是统一建模语言，AUTOSAR元模型是UML2.0模型（2.0基于1.x，对结构类、精确的接口和端口、拓展性、交互片断和操作符以及基于时间建模能力做了增强）。
  >
  > 使用UML定义的AUTOSAR Meta-model没有太大必要单独去看，因为所有相关信息和图表都会在AUTOSAR Template Specification里有。下图是基于EA打开的`AUTOSAR_MMOD_MetaModel.zip`,可以看到各种UML图
  >
  > ![image-20221222113228556](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212221132667.png)
  >
  > <h5 align="center">AUTOSAR_MMOD_MetaModel</h5>

- **MOD：**model，介绍基于元模型建模的原理，一般指的是如下的arxml，该标准介绍了如何将[AUTOSAR](https://so.csdn.net/so/search?q=AUTOSAR&spm=1001.2101.3001.7020)模型序列化为AUTOSAR XML描述的规则，为AUTOSAR工具之间的互操作性提供支持。

  ![XML模式生成规则和ARXML序列化规则之间的关系](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212221147572.png)

  - AUTOSAR_MOD_GeneralDefinitions.zip
  - AUTOSAR_MOD_MiscSupport.zip
  - AUTOSAR_MOD_GeneralBlueprints.zip
  - AUTOSAR_MOD_BSWUMLModel.zip
  - AUTOSAR_MOD_ECUConfigurationParameters.zip
  - AUTOSAR_MOD_AdaptivePlatformGeneralBlueprints.zip

  例如所有安全事件定义集中在**AUTOSAR_MOD_GeneralDefinition_SecurityEvents.arxml**文件中

  ![image-20221222113513931](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212221135955.png)

  <h5 align="center">AUTOSAR_MOD_GeneralDefinitions.zip</h5>

- **RS：**Requirement Specification，需求规范，层次比SRS要高，比如AUTOSAR_RS_Main.pdf中对架构、基础软件、方法论等进行了明确的规范(如下图所示)。

  | ![image-20221222133037990](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212221330025.png) | ![image-20221222133231764](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212221332806.png) |
  | :----------------------------------------------------------: | :----------------------------------------------------------: |
  |                       **文档需求规范**                       |                       **需求规范示例**                       |

 

- **TR：**Technical Report，技术报告，比如AUTOSAR_TR_PredefinedNames.pdf用于对不同的缩写进行了说明。

- **TPS：**Template Specification，模板规范，用于介绍模块的处理架构、层次关系等，比如下图对诊断事件的层次结构进行的规范(如下图所示)。

  ![image-20221222140238410](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212221402466.png)

- **EXP：**Explaination，说明文档，**对其他文档中提到的内容**进行解释说明。

  - 例如AUTOSAR_EXP_LayeredSoftwareArchitecture.pdf，这是非常非常重要的一部分，大多的基础概念来自于这个文档。

- **SRS：**Software Requirement Specification，软件需求规范，用于对各个软件模块功能需求进行说明。例如AUTOSAR_SRS_OS，定义了OS的各类需求，包括需求来源

  ![image-20221222135617188](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212221356226.png)

  <h5 align="center">图示:AUTOSAR_SRS_OS.pdf SRS需求定义</h5>

- **SWS**：Software Specification，软件规范，详细介绍模块设计和实现原理，包括模块功能的详细介绍，API接口介绍，数据类型介绍，软件的流程图(如下图所示)，**一般软件开发，重点我们看这个文档**

  ![image-20221222134056534](https://imgs-1251682926.cos.ap-shanghai.myqcloud.com/autosar/202212221340571.png)

<h5 align="center">图示:AUTOSAR_SWS_OS.pdf 软件设计定义</h5>





**如何阅读？**

对于大部分基于工具的AutoSAR工作者来说，只需要看SWS即可；一般来说，对于工具开发商而言，其也会提供一套参考文档（比如Vector公司提供的文档位于TechnicalReferences下）。对于AutoSAR工具的开发者而言，或者一些需要手写AutoSAR代码的，就需要按需求深入理解文档了。



**为什么不建议通读？**

闲来无聊，统计了一下文档的页数：

```python
# !/usr/bin/env python3
import argparse
from glob import glob
from os.path import exists, join
from PyPDF2 import PdfFileReader


def get_total_pages(folder):
    if not exists(folder):
        return "文件目录: {}  不存在".format(folder)
    pdf_list = glob(join(folder, "*.pdf"))

    pages = []
    for pdf in pdf_list:
        reader = PdfFileReader(pdf)
        num_page = reader.getNumPages()
        pages.append(num_page)
    return [sum(pages), len(pdf_list)]


if __name__ == "__main__":
    parser = argparse.ArgumentParser()
    parser.add_argument('folder', type=str, help='输入文件路径')
    args = parser.parse_args()
    [total_pages, files] = get_total_pages(args.folder)

    print("'%s'\n 文件数: %d  总页数:%d " % (args.folder, files, total_pages))

```



| 类型               | 版本  | 文件数 | 总页数    |
| ------------------ | ----- | ------ | --------- |
| classic经典平台    | 22-11 | 210    | 21913     |
| foundation基础     | 22-11 | 49     | 2876      |
| adaptive自适应平台 | 22-11 | 39     | 2511      |
|                    |       | 298    | **27300** |

>  按照A4纸每页0.104mm的厚度计算，27300页单面打印出来**2.8米**高，





## 三、AUTOSAR文档阅读建议

> CP文档的阅读：

**一般性文档**

- AUTOSAR_EXP_VFB  虚拟总线，建议从这个了解SWC开发

- AUTOSAR_EXP_LayeredSoftwareArchitecture 整体 Overview，建议从这份文档开始学习

##### 详细了解文档：

- AUTOSAR_SWS_OS  autosar OS的描述
- AUTOSAR_SWS_RTE  运行时环境
- AUTOSAR_SWS_COM    通讯模块
- AUTOSAR_SWS_BSWGeneral BSW模块的规范
- AUTOSAR_TR_Methodology   CP 方法论

>  AP 部分

##### 一般性文档

- AUTOSAR_EXP_PlatformDesign：整体 Overview，建议从这份文档开始学习
- AUTOSAR_EXP_SWArchitecture：软件架构
- AUTOSAR_EXP_AdaptivePlatformInterfacesGuidelines：接口使用指引
- AUTOSAR_EXP_ARAComAPI：通信管理API

##### 有些 High-level 文档可以先快速浏览，用到的时候再细看：

- AUTOSAR_TR_FunctionalClusterShortnames：各个 FC 的缩写
- AUTOSAR_RS_General：编码风格指南
- AUTOSAR_RS_CPP14Guidelines：MISRA C++ 编码规范，已废弃，之后交给 MISRA 维护，不再由 AUTOSAR 维护
- AUTOSAR_TPS_ManifestSpecification：Manifest 规范
- AUTOSAR_TR_AdaptiveMethodology：AP方法论
- AUTOSAR_RS_OperatingSystemInterface：操作系统接口
- AUTOSAR_SWS_AdaptiveCore

如果你不知道从哪份文档开始阅读，我建议可以从这份开始 AUTOSAR_EXP_PlatformDesign.pdf
