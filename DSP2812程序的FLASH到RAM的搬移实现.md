# DSP2812程序的FLASH到RAM的搬移实现（NonBIOS）

## 1.实验环境：

-  HelloDSP的DSP2812的开发板
-  源程序使用的是HelloDSP提供的源程序（库文件有更改）
- 开发环境：CCS3.3

## 2.实验要点：

1. code_start：asm文件，关闭看门狗之后，跳转到程序复制代码部分（copy_sections），执行完毕后跳转到copy_sections。
2. copy_sections：asm文件，将定义的程序段从FLASH搬移到RAM，需要自己定义搬移用到的地址、程序大小变量，并且添加自定义搬移段的搬移代码（模仿即可），执行完毕后跳转到_c_init00。
3. 将HelloDSP提供的库文件rts2800_fl040830.lib替换为TI提供的rts2800.lib。因为HelloDSP提供的库文件中存在代码搬移部分（将.const与.econst段从FLASH搬移到RAM，并且使用了用于搬移的变量。观察HelloDSP提供的FLASH.cmd文件可以发现，其中定义了用于搬移的变量。
4. TI提供的code_start与copy_sections程序中可能跳转语句与期望的不同，需要调整LB指令后面的地址，完成在上电后自动将程序搬移到RAM。
5. cmd文件需要定义好loadstart、runstart、size等变量，同时划分好程序空间与内存空间。
6. 程序运行顺序：
   1. 从ROM中的Boot程序启动，根据IO管脚状态，选择从0x3f7ff6启动
   2. 0x3f7ff6中储存了跳转指令，跳转到code_start代码部分
   3. code_start代码部分屏蔽看门狗，并且跳转到copy_sections代码部分
   4. copy_sections完成代码段从FLASH到RAM的复制，完成后跳转到_c_init00
   5. _c_init00完成程序初始化操作，完毕后跳转到main函数
   6. 开始在RAM中执行main函数
7. 在实际操作过程中，IQmath程序部分从FLASH搬移到RAM中出现失败，通过观察DSP内部FLASH与RAM中的内容，发现IQmath部分并没有复制成功。

## 3.实验感悟

1. 磨刀不误砍柴功。自己之前并没有认真地了解DSP的工作原理，所以遇到问题总是倒推来找原因，头痛医头，脚痛医脚，不观全局，前后断断续续一个星期才弄好。
2. TI官方文档真的写得很好，但是要耐下心来看。

作者：donghao@Lab209

时间：2016.9.12

邮箱：dongyinhao@foxmail.com