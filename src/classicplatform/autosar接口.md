# AUTOSAR的接口

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