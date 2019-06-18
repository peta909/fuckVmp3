# 这是什么？
几年前写的`vmp3` `handle`分析脚本。  
这是最初的代码，换了几次硬盘后，后来的找不到了。今天发现这个最早的古董，索性放上来吧。
可能现在已经比较落后了，但是在`vmp`能带来的巨大的商业价值的当时(也可能包括现在),这方面的资料还是比较少的。
作为抛砖引玉吧。

# 都有什么功能
实现了以下vmp handle的识别和转换

|指令|用途
|:-|:-
|vPopReg4|将栈中的`4`字节数据存入参数指定的寄存器
|vPopReg2| ..
|vPopReg1|..
|vPushReg4|将指定寄存器的入栈
|vReadMem4|读取段4字节内存,以栈顶4字节为地址读取4字节内容保存到栈顶
|vWriteMemSs4|写入SS段4字节内存,以栈顶4字节为地址，栈顶+4 4字节为内容写入SS段内存，弹出8字节
|vAdd4|4字节加法,栈顶4字节和栈顶+4 4字节相加，结果保存到栈顶+4，标志4字节保存到栈顶
|vAdd2|2字节加法,栈顶2字节和栈顶+2 2字节相加，压入2字节后把结果保存到栈顶+4，标志4字节保存到栈顶
|vPopVEsp|弹出vESP，把栈顶4字节弹出到vESP（栈顶指针）
|vPushImm4|4字节立即数压栈，从指令中取出4字节立即数压入栈顶
|vPushImm2|..
|vNand4|4字节与非，栈顶4字节和栈顶+4 4字节做与非运算，结果保存到栈顶+4，标志4字节保存到栈顶，即`not not and`，逻辑闸，vmp通过此指令来模拟逻辑运算。
|vNand2|..
|vShl4|4字节逻辑左移,栈顶4字节内容，栈顶+4 2字节作为1字节移位数做逻辑左移，压入2字节后把结果保存到栈顶+4，标志4字节保存到栈顶
|vShl1|..
|vShl2|..
|vShr4|..
|vShr2|..
|vShr1|..

# 适用于哪个版本?
已测试适配vmp3.0.59


## 还需要做什么？
其实下面的之前都已经弄好了，但是后来我主要从事移动端的工作，时间长代码都弄丢了。。  
* IR转换
* 逻辑闸优化


这里提供下思路,先转换成ir，然后再通过编译器优化去掉多余的逻辑闸即可。