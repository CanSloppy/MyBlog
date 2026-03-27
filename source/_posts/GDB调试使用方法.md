---
title: GDB调试使用方法
date: 2025-02-13 16:41:43
tags: 'Linux命令'
categories: 'Linux'
---

## GDB安装教程

首先查看自己有没有安装GDB，如果没有安装则需要先安装

```plain
sudo apt install gdb
gdb --version
```

## 使用方法
在安装完成后，对指定的可执行程序前增加gdb即可进入调试状态如图

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2025/png/53234367/1741848182644-a5c0bb17-612a-4b46-b56b-272cb4e81069.png)

显示如下状态则说明gdb启动程序成功，就可以对程序进行调试了！

## 基础命令
注：（）括号里面是该指令的全称 

l(list) 行号/函数名 —— 显示对应的code，每次10行  

r(run) —— F5【无断点直接运行、有断点从第一个断点处开始运行】  

b(breakpoint) + 行号 —— 在那一行打断点  

b 源文件：函数名 —— 在该函数的第一行打上断点  

b 源文件：行号 —— 在该源文件中的这行加上一个断点吧  

info b —— 查看断点的信息  

d(delete) + 当前要删除断点的编号 —— 删除一个断点【不可以d + 行号】  

若当前没有跳出过gdb，则断点的编号会持续累加  
d + breakpoints —— 删除所有的断点  

disable b(breakpoints) —— 使所有断点无效【默认缺省】  

enable b(breakpoints) —— 使所有断点有效【默认缺省】  

disable b(breakpoint) + 编号 —— 使一个断点无效【禁用断点】  

enable b(breakpoint) + 编号 —— 使一个断点有效【开启断点】  

相当于VS中的空断点  
enable breakpount —— 使一个断点有效【开启断电】  

n(next) —— 逐过程【相当于F10，为了查找是哪个函数出错了】  

s(step) —— 逐语句【相当于F11，】  

bt —— 看到底层函数调用的过程【函数压栈】  

set var —— 修改变量的值  

p(print) 变量名 —— 打印变量值  

display —— 跟踪查看一个变量，每次停下来都显示它的值【变量/结构体…】  

undisplay + 变量名编号 —— 取消对先前设置的那些变量的跟踪

## 排查问题三剑客🗡
until + 行号 —— 进行指定位置跳转，执行完区间代码



finish —— 在一个函数内部，执行到当前函数返回，然后停下来等待命令



c(continue) —— 从一个断点处，直接运行至下一个断点处【VS下不断按F5】

## <font style="color:rgb(51, 51, 51);">GDB命令大全</font>
**<font style="color:rgb(51, 51, 51);">list</font>**<font style="color:rgb(51, 51, 51);"> ：显示程序中的代码，常用使用格式有： list 输出从上次调用list命令开始往后的10行程序代码。 list - 输出从上次调用list命令开始往前的10行程序代码。 list n 输出第n行附近的10行程序代码。 list function 输出函数function前后的10行程序代码。</font>

**<font style="color:rgb(51, 51, 51);">forward/search</font>**<font style="color:rgb(51, 51, 51);"> ：从当前行向后查找匹配某个字符串的程序行。使用格式： forward/search 字符串 查找到的行号将保存在$</font>_<font style="color:rgb(51, 51, 51);">变量中，可以用print $</font>_<font style="color:rgb(51, 51, 51);">命令来查看。</font>

**<font style="color:rgb(51, 51, 51);">reverse-search</font>**<font style="color:rgb(51, 51, 51);"> ：和forward/search相反，向前查找字符串。使用格式同上。</font>

**<font style="color:rgb(51, 51, 51);">break</font>**<font style="color:rgb(51, 51, 51);"> ：在程序中设置断点，当程序运行到指定行上时，会暂停执行。使用格式：</font><font style="color:rgb(51, 51, 51);"> break 要设置断点的行号</font>

**<font style="color:rgb(51, 51, 51);">tbreak</font>**<font style="color:rgb(51, 51, 51);"> ：设置临时断点，在设置之后只起作用一次。使用格式：</font><font style="color:rgb(51, 51, 51);"> tbreak 要设置临时断点的行号</font>

**<font style="color:rgb(51, 51, 51);">clear</font>**<font style="color:rgb(51, 51, 51);"> ：和break相反，clear用于清除断点。使用格式：</font><font style="color:rgb(51, 51, 51);"> clear 要清除的断点所在的行号</font>

**<font style="color:rgb(51, 51, 51);">run</font>**<font style="color:rgb(51, 51, 51);"> ：启动程序，在run后面带上参数可以传递给正在调试的程序。</font>

**<font style="color:rgb(51, 51, 51);">awatch</font>**<font style="color:rgb(51, 51, 51);"> ：用来增加一个观察点(add watch)，使用格式：</font><font style="color:rgb(51, 51, 51);"> awatch 变量或表达式</font><font style="color:rgb(51, 51, 51);"> 当表达式的值发生改变或表达式的值被读取时，程序就会停止运行。</font>

**<font style="color:rgb(51, 51, 51);">watch</font>**<font style="color:rgb(51, 51, 51);"> ：与awatch类似用来设置观察点，但程序只有当表达式的值发生改变时才会停止运行。使用格 式：</font><font style="color:rgb(51, 51, 51);"> watch 变量或表达式</font><font style="color:rgb(51, 51, 51);"> 需要注意的是，awatch和watch都必须在程序运行的过程中设置观察点，即可运行run之后才能设置。</font>

**<font style="color:rgb(51, 51, 51);">commands</font>**<font style="color:rgb(51, 51, 51);"> ：设置在遇到断点后执行特定的指令。使用格式有：</font><font style="color:rgb(51, 51, 51);"> commands</font><font style="color:rgb(51, 51, 51);"> 设置遇到最后一个遇到的断点时要执行的命令</font><font style="color:rgb(51, 51, 51);"> commands n</font><font style="color:rgb(51, 51, 51);"> 设置遇到断点号n时要执行的命令</font><font style="color:rgb(51, 51, 51);"> 注意，commands后面跟的是断点号，而不是断点所在的行号。</font><font style="color:rgb(51, 51, 51);"> 在输入命令后，就可以输入遇到断点后要执行的命令，每行一条命令，在输入最后一条命令后输入end就可以结束输入。</font>

**<font style="color:rgb(51, 51, 51);">delete</font>**<font style="color:rgb(51, 51, 51);"> ：清除断点或自动显示的表达式。使用格式：</font><font style="color:rgb(51, 51, 51);"> delete 断点号</font>

**<font style="color:rgb(51, 51, 51);">disable</font>**<font style="color:rgb(51, 51, 51);"> ：让指定断点失效。使用格式：</font><font style="color:rgb(51, 51, 51);"> disable 断点号列表</font><font style="color:rgb(51, 51, 51);"> 断点号之间用空格间隔开。</font>

**<font style="color:rgb(51, 51, 51);">enable</font>**<font style="color:rgb(51, 51, 51);"> ：和disable相反，恢复失效的断点。使用格式：</font><font style="color:rgb(51, 51, 51);"> enable 断点编号列表</font>

**<font style="color:rgb(51, 51, 51);">ignore</font>**<font style="color:rgb(51, 51, 51);"> ：忽略断点。使用格式：</font><font style="color:rgb(51, 51, 51);"> ignore 断点号 忽略次数</font>

**<font style="color:rgb(51, 51, 51);">condition</font>**<font style="color:rgb(51, 51, 51);"> ：设置断点在一定条件下才能生效。使用格式：</font><font style="color:rgb(51, 51, 51);"> condition 断点号 条件表达式</font>

**<font style="color:rgb(51, 51, 51);">cont/continue</font>**<font style="color:rgb(51, 51, 51);"> ：使程序在暂停在断点之后继续运行。使用格式：</font><font style="color:rgb(51, 51, 51);"> cont</font><font style="color:rgb(51, 51, 51);"> 跳过当前断点继续运行。</font><font style="color:rgb(51, 51, 51);"> cont n</font><font style="color:rgb(51, 51, 51);"> 跳过n次断点，继续运行。</font><font style="color:rgb(51, 51, 51);"> 当n为1时，cont 1即为cont。</font>

**<font style="color:rgb(51, 51, 51);">jump</font>**<font style="color:rgb(51, 51, 51);"> ：让程序跳到指定行开始调试。使用格式：</font><font style="color:rgb(51, 51, 51);"> jump 行号</font>

**<font style="color:rgb(51, 51, 51);">next</font>**<font style="color:rgb(51, 51, 51);"> ：继续执行语句，但是跳过子程序的调用。使用格式：</font><font style="color:rgb(51, 51, 51);"> next</font><font style="color:rgb(51, 51, 51);"> 执行一条语句</font><font style="color:rgb(51, 51, 51);"> next n</font><font style="color:rgb(51, 51, 51);"> 执行n条语句</font>

**<font style="color:rgb(51, 51, 51);">nexti</font>**<font style="color:rgb(51, 51, 51);"> ：单步执行语句，但和next不同的是，它会跟踪到子程序的内部，但不打印出子程序内部的语句。使用格式同上。</font>

**<font style="color:rgb(51, 51, 51);">step</font>**<font style="color:rgb(51, 51, 51);"> ：与next类似，但是它会跟踪到子程序的内部，而且会显示子程序内部的执行情况。使用格式同上。</font>

**<font style="color:rgb(51, 51, 51);">stepi</font>**<font style="color:rgb(51, 51, 51);"> ：与step类似，但是比step更详细，是nexti和step的结合。使用格式同上。</font>

**<font style="color:rgb(51, 51, 51);">whatis</font>**<font style="color:rgb(51, 51, 51);"> ：显示某个变量或表达式的数据类型。使用格式：</font><font style="color:rgb(51, 51, 51);"> whatis 变量或表达式</font>

**<font style="color:rgb(51, 51, 51);">ptype</font>**<font style="color:rgb(51, 51, 51);"> ：和whatis类似，用于显示数据类型，但是它还可以显示typedef定义的类型等。使用格式：</font><font style="color:rgb(51, 51, 51);"> ptype 变量或表达式</font>

**<font style="color:rgb(51, 51, 51);">set</font>**<font style="color:rgb(51, 51, 51);"> ：设置程序中变量的值。使用格式：</font><font style="color:rgb(51, 51, 51);"> set 变量=表达式</font><font style="color:rgb(51, 51, 51);"> set 变量:=表达式</font>

**<font style="color:rgb(51, 51, 51);">display</font>**<font style="color:rgb(51, 51, 51);"> ：增加要显示值的表达式。使用格式：</font><font style="color:rgb(51, 51, 51);"> display 表达式</font>

**<font style="color:rgb(51, 51, 51);">info display</font>**<font style="color:rgb(51, 51, 51);"> ：显示当前所有的要显示值的表达式。</font>

**<font style="color:rgb(51, 51, 51);">delete display/undisplay</font>**<font style="color:rgb(51, 51, 51);"> ：删除要显示值的表达式。使用格式：</font><font style="color:rgb(51, 51, 51);"> delete display/undisplay 表达式编号</font>

**<font style="color:rgb(51, 51, 51);">disable display</font>**<font style="color:rgb(51, 51, 51);"> ：暂时不显示一个要表达式的值。使用格式：</font><font style="color:rgb(51, 51, 51);"> disable display 表达式编号</font>

**<font style="color:rgb(51, 51, 51);">enable display</font>**<font style="color:rgb(51, 51, 51);"> ：与disable display相反，使用表达式恢复显示。使用格式：</font><font style="color:rgb(51, 51, 51);"> enable display 表达式编号</font>

**<font style="color:rgb(51, 51, 51);">print</font>**<font style="color:rgb(51, 51, 51);"> ：打印变量或表达式的值。使用格式：</font><font style="color:rgb(51, 51, 51);"> print 变量或表达式</font><font style="color:rgb(51, 51, 51);"> 表达式中有两个符号有特殊含义：$和</font>

<font style="color:rgb(51, 51, 51);">。 $表示给定序号的前一个序号，。 $表示给定序号的前一个序号，</font>

<font style="color:rgb(51, 51, 51);">表示给定序号的前两个序号。</font><font style="color:rgb(51, 51, 51);"> 如果$和$$后面不带数字，则给定序号为当前序号。</font>

**<font style="color:rgb(51, 51, 51);">backtrace</font>**<font style="color:rgb(51, 51, 51);"> ：打印指定个数的栈帧(stack frame)。使用格式：</font><font style="color:rgb(51, 51, 51);"> backtrace 栈帧个数</font>

**<font style="color:rgb(51, 51, 51);">frame</font>**<font style="color:rgb(51, 51, 51);"> ：打印栈帧。使用格式：</font><font style="color:rgb(51, 51, 51);"> frame 栈帧号</font>

**<font style="color:rgb(51, 51, 51);">info frame</font>**<font style="color:rgb(51, 51, 51);"> ：显示当前栈帧的详细信息。</font>

**<font style="color:rgb(51, 51, 51);">select-frame</font>**<font style="color:rgb(51, 51, 51);"> ：选择栈帧，选择后可以用info frame来显示栈帧信息。使用格式：</font><font style="color:rgb(51, 51, 51);"> select-frame 栈帧号</font>

**<font style="color:rgb(51, 51, 51);">kill</font>**<font style="color:rgb(51, 51, 51);"> ：结束当前程序的调试。</font>

**<font style="color:rgb(51, 51, 51);">quit</font>**<font style="color:rgb(51, 51, 51);"> ：退出gdb。</font>

