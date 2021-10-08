---
layout: post
title: 虚拟化技术
categories: Visualization
description: 虚拟化技术 docker 
keywords: 虚拟化  
---

##### 常见虚拟化技术概念解析：

1.虚拟化：一种形式的资源抽象成另一种形式的技术 例如虚存技术

2.Virtual Machine，简称VM：即虚拟机，它所抽象的是整个物理机，包括CPU、内存和I/O设备

3.VMM(Virtual Machine Monitor):提供虚拟化的平台

4.Guest VM:在VMM上运行的虚机

5.Guest VM的运行方式：完全虚拟化（Full Virtualization）和类虚拟化（Para Virtualization）

6.完全虚拟化：VMM需要正确处理guest所有可能的指令

​	最简单直接的方法就是，VMM对guest运行过程中的每一条指令都进行解释和执行，模拟出这条指令执行的效果，这种方法既适用于和VMM相同体系结构的guest，也能用于模拟和VMM不同体系结构的guest（比如物理CPU是x86的，而guest是基于ARM的），其缺点也很明显，就是性能太差。

​	但是有一些指令是要操作特权资源的，比如修改虚拟机的运行模式或者下面物理机的状态，读写时钟或者中断寄存器，这些指令被称为敏感指令，确实不适合由guest直接来控制。

​	然而其他的一些非敏感指令，是完全可以在物理CPU上直接执行并返回结果给guest的，VMM只需要截获并模拟guest对敏感指令的执行和对特权资源的访问就可以了，以intel的VT-x和AMD的AMD-V为代表的硬件辅助虚拟化技术，就可以帮助VMM高效地识别和截获这些敏感指令。【1】

7：类虚拟化：

通过二进制代码翻译（binary translation），扫描并修改guest的二进制代码将难以虚拟化的指令转换成支持虚拟化的指令

##### 虚拟化技术架构：

1.**Hypervisor模型**

具备传统操作系统的功能，还具备虚拟化功能。包括CPU、内存和I/O设备在内的所有物理资源都归VMM所有，因此VMM不仅要负责虚拟机环境的创建和管理，还承担着管理物理资源的责任。

2.**Host模型**

物理资源由宿主机管理，虚拟化功能由VMM调度，VMM创建出的虚机只是Host主机的一个进程参与调度

3.**混合模型**

混合模型，结合上述两种模型，VMM拥有所有物理资源，但是I/O设备由一个Service OS接管，运行在特权级别，自己主要负责CPU管理和内存管理。

