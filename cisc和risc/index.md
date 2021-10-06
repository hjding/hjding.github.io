# CISC和RISC


## 精简指令集(Reduced Instruction Set Computer, RISC)

这种CPU的设计中，微指令集较为精简，每个指令的运行时间都很短，完成的动作也很单纯，指令的执行效能较佳； 但是若要做复杂的事情，就要由多个指令来完成。常见的RISC 微指令集CPU 主要例如甲骨文(Oracle) 公司的SPARC 系列、IBM 公司的Power Architecture (包括PowerPC) 系列、与安谋公司(ARM Holdings) 的ARM CPU 系列等。

## 复杂指令集(Complex Instruction Set Computer, CISC)

在CISC在微指令集中，每个小指令可以执行一些较低阶的硬件操作，指令数目多而且复杂，每条指令的长度并不相同。因为指令执行较为复杂所以每条指令花费的时间较长， 但每条个别指令可以处理的工作较为丰富。常见的CISC微指令集CPU主要有AMD、Intel、VIA 等的x86 架构的CPU。

## CISC和RISC的区别

1. CISC的指令能力强，单多数指令使用率低却增加了CPU的复杂度，指令是可变长格式；RISC的指令大部分为单周期指令，指令长度固定，操作寄存器，只有Load/Store操作内存
2. CISC支持多种寻址方式；RISC支持方式少
3. CISC通过微程序控制技术实现；RISC增加了通用寄存器，硬布线逻辑控制为主，4. 是和采用流水线
4. CISC的研制周期长
5. RISC优化编译，有效支持高级语言
