> 贡献名单：U202340627 +2

# vscode配置C/C++环境

## 让我们开始

首先我们需要安装vscode本体，这个在这里就不用过多赘述，大家百度下载即可

安装完成后打开，看到的应该是差不多下面这样的一个界面

![image-20250331145450321](../assets/img/basic-knowledge/VScode/image-20250331145450321.png)



## 中文汉化（可选

打开软件后铺面而来的英文可能让你略感恍惚，不必紧张，打开左侧边栏从上往下数第五个图标，来到扩展商店，随后在搜索栏键入 chinese (键入ch都行) 找到vscode中文汉化扩展，点击 install 下载

![image-20250331145727707](../assets/img/basic-knowledge/VScode/image-20250331145727707.png)



install 完成以后，右下角会弹出弹窗询问我们是否要立即切换为简体中文并且重启vscode(切换语言需要重启)，我们点击 `Change Language and Restart` ，等待vscode重新开启以后就可以得到一个中文界面

![image-20250331145821861](../assets/img/basic-knowledge/VScode/image-20250331145821861.png)

![image-20250331150016522](../assets/img/basic-knowledge/VScode/image-20250331150016522.png)



## 配置C/C++单文件运行/调试环境

### 下载工具并且配置PAYH (vscode以外)

做完上面的步骤以后我们手中的vscode还只是一个比较美观的文本编辑器，为了让它拥有更多更强大的功能，让它能够编译运行我们写的C/C++代码，我们需要接入编译器 gcc 和 g++ 调试器 gdb等工具。

我们使用msys2来安装我们需要的工具[^1]，[官网访问点这里](https://www.msys2.org/)(这是msys2官网，进去以后就能看到 Download the installer 不过它也是要跳转到github那边去下载的，所以也需要魔法)，  [下载链接点这里](https://github.com/msys2/msys2-installer/releases/) (这是github上的 魔法/watt toolkit自备)

github上的进来以后点最新的日期就可以跳转到资料列表，在列表中找到对应系统的安装包下载(大多数人都是windows所以我们这里选择.exe进行安装演示)

![image-20250331151614173](../assets/img/basic-knowledge/VScode/image-20250331151614173.png)

![image-20250331151724301](../assets/img/basic-knowledge/VScode/image-20250331151724301.png)



下载完成以后双击启动安装程序

|                           点击next                           |              选择你要安装到的位置(==后面要考==)              |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
| <img src="../assets/img/basic-knowledge/VScode/image-20250331152545940.png" alt="image-20250331152545940" style="zoom:50%;" /> | <img src="../assets/img/basic-knowledge/VScode/image-20250331152655716.png" alt="image-20250331152655716" style="zoom:50%;" /> |

|        要不要再开始菜单中创建快速访问->随便 next就行         |               等待安装(慢慢等) 安装完后点next                |                    点击Finish，运行msys2                     |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
| ![image-20250331152828442](../assets/img/basic-knowledge/VScode/image-20250331152828442.png) | ![image-20250331153007009](../assets/img/basic-knowledge/VScode/image-20250331153007009.png) | ![image-20250331154055737](../assets/img/basic-knowledge/VScode/image-20250331154055737.png) |



如果你上面最后一步不小心把勾取消了、不小心把程序直接叉掉了 ~~那很不小心了~~ 没关系，可以按windows键，就是键盘上左下角(右下角也可能有)的一个有四个小正方形组成一个大正方形的图标。点一下，输入msys后，如下图，打开

<img src="../assets/img/basic-knowledge/VScode/image-20250331155312030.png" alt="image-20250331155312030" style="zoom:67%;" />



在这终端里输入 `pacman -S --needed base-devel mingw-w64-ucrt-x86_64-toolchain` 安装需要的工具

| 直接回车 安装所有                                            | 输入 Y 继续安装                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![image-20250331155404467](../assets/img/basic-knowledge/VScode/image-20250331155404467.png) | ![image-20250331155431795](../assets/img/basic-knowledge/VScode/image-20250331155431795.png) |



只需等待……

![image-20250331155457360](../assets/img/basic-knowledge/VScode/image-20250331155457360.png)



这样表示所有包都安装好了，直接关闭终端即可

<img src="../assets/img/basic-knowledge/VScode/image-20250331155718197.png" alt="image-20250331155718197" style="zoom: 67%;" />

**接下来是配置环境变量**

Q:为什么要配置？

A:为了让你的vscode能在茫茫电脑文件中一眼看到它想要的工具  （

首先找到我们刚刚安装的包的二进制文件目录，这里面有着很多工具。该文件夹位于你安装msys2目录下的ucrt64\bin，在我这里就是下图，复制bin文件夹的地址

![image-20250331160132535](../assets/img/basic-knowledge/VScode/image-20250331160132535.png)



按下windows键，输入”环境变量“几个字，找到并打开 “编辑系统环境变量”

![image-20250331160323643](../assets/img/basic-knowledge/VScode/image-20250331160323643.png)

|                         点击环境变量                         |                      选择Path，点击编辑                      |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
| ![image-20250331160649059](../assets/img/basic-knowledge/VScode/image-20250331160649059.png) | ![image-20250331160827994](../assets/img/basic-knowledge/VScode/image-20250331160827994.png) |

|     选择新建，将刚刚找到的路径粘贴到新建栏目中，点击确定     |                          接着点确定                          |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
| ![image-20250331161035205](../assets/img/basic-knowledge/VScode/image-20250331161035205.png) | ![image-20250331161207911](../assets/img/basic-knowledge/VScode/image-20250331161207911.png) |



好了，现在已经完成了环境变量的配置，我们可以用终端来验证一下电脑知不知道它有这个工具

按住 `windows+r` 键，输入cmd运行终端，随后在终端中输入 `g++ --version`等(一个就够)， 如果你的电脑能输出类似下面的信息，恭喜你，完美完成了以上的任务！

![image-20250331161501434](../assets/img/basic-knowledge/VScode/image-20250331161501434.png)



### vscode中的配置

打开vscode，在扩展商店中输入C++，安装图示的两款扩展

![image-20250331161845131](../assets/img/basic-knowledge/VScode/image-20250331161845131.png)



安装完以后，我们~~随便~~打开一个文件夹，创建一个文件test.cpp，并且尝试输出一下hello world。==记得信任你的文件夹来让打开他们的时候也能使用扩展喵==  **如果你的文件报错 请确认你的代码是否出现错误 如果没有 重启vscode**

选择右上角的运行C/C++文件

![image-20250331162456056](../assets/img/basic-knowledge/VScode/image-20250331162456056.png)



如果你写的是C，选择gcc的那个；如果你写的是C++，选择g++的那个，然后观察

![image-20250331162558721](../assets/img/basic-knowledge/VScode/image-20250331162558721.png)

![image-20250331162944774](../assets/img/basic-knowledge/VScode/image-20250331162944774.png)



此时我们已经可以正常的进行单文件编译运行与调试，按F5或者在右上角选择调试C/C++文件，调试细节这里不作展开

![image-20250331163412826](../assets/img/basic-knowledge/VScode/image-20250331163412826.png)



## 配置C/C++多文件运行/调试环境

如果你想要进行多文件运行/调试，那就需要下面的进一步设置

![image-20250331172052447](../assets/img/basic-knowledge/VScode/image-20250331172052447.png)


此时会自动打开刚刚创建的launch文件，并且展开配置选项给我们选择，如果~~不小心~~关掉了可以点右下角的<添加配置>来展开这个列表。

选择  (gdb)启动 后就会生成一段默认的json内容

![image-20250331172422504](../assets/img/basic-knowledge/VScode/image-20250331172422504.png)



launch.json中最少需要修改的内容只有两项，如下图

![image-20250331172721136](../assets/img/basic-knowledge/VScode/image-20250331172721136.png)



第一项为你编译完多文件以后的二进制文件(exe文件)名称，这里我们按下不表，需要task.json中修改一些配置再来。第二项为调试程序的位置，它的位置在我们安装msys2目录下的 `ucrt64\bin` 文件夹，这里我们需要复制gdb.exe文件的绝对地址填入上面的第二项中。(如何获得绝对地址呢？ 右键gdb.exe程序在菜单中选择复制文件地址)

![image-20250331172950849](../assets/img/basic-knowledge/VScode/image-20250331172950849.png)

如果你按照我说的直接复制文件地址并且粘贴到第二项的位置的话，现在可能是这个情况。

![image-20250331173201711](../assets/img/basic-knowledge/VScode/image-20250331173201711.png)



这个情况有两个错误

1. 两边有两对双引号，多了一对。需要删除
2. 单个\表示转义，两个\才表示\，所以要加一个\

修改后

![image-20250331173906222](../assets/img/basic-knowledge/VScode/image-20250331173906222.png)



现在对于第一处要改的，我们来看task.json  (在打开文件夹的 .vscode文件夹中你可以看到launch.json和task.json)

task.json最少需要修改的也是两处，如下图

![image-20250331174632244](../assets/img/basic-knowledge/VScode/image-20250331174632244.png)

第一处表示编译的文件，原本的 `${file}` 表示编译当前文件，现在我们需要编译多文件，即编译当前目录下的所有 C/C++ 文件，所以我们将它修改为

​	一 一列出所有参与编译的cpp文件。比如 a.cpp b.cpp c.cpp都参与编译就要列为

```json
"a.cpp",
"b.cpp",
"c.cpp",
```

==**注意头文件不需要列出**==



第二处表示生成的可执行程序名，原本的

​					`${fileDirname}\\${fileBasenameNoExtension}.exe`

表示 **当前目录下的**、**编译的文件去掉后缀名(也就是.cpp或者.c这种)** 作为**文件名** ， .exe作为**扩展名**

那我们编译多文件的时候这样命名必然存在冲突，因为有很多文件被编译，所以不能确定到底是哪个名字

所以我们需要将最后的可执行文件单独命名，比如直接叫做 `main.exe`

按照上面说的修改后(我的参与编译的cpp文件看左边 是sum.cpp和test.cpp)：

![image-20250331185245461](../assets/img/basic-knowledge/VScode/image-20250331185245461.png)



好了，<u>你是否还记得launch.json文件里还有一处没改？</u>

没改的一处是让我们输入程序名称，我们在task.json里已经对最终的名称进行了命名，也就是task.json里的第二处修改 `${fileDirname}\\main.exe` 我们把这个命名复制到launch.json里的第一处需要修改的地方即可，下面给出两处全部修改的launch.json

![image-20250331180355933](../assets/img/basic-knowledge/VScode/image-20250331180355933.png)



下面我们简单测试一下能否进行多文件运行和调试

| 调试                                                         | 运行                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![image-20250331185943036](../assets/img/basic-knowledge/VScode/image-20250331185943036.png) | ![image-20250331190008570](../assets/img/basic-knowledge/VScode/image-20250331190008570.png) |



## 更进一步

上面的多文件运行与调试每次都需要把目标文件写进task.json，实在麻烦

实际上，我们可以采用“*.cpp”来一次性表示所有的cpp文件，从而做到不需要每次都调整task.json文件。**然鹅**，==g++编译器无法处理通配符！！！== 如果想进一步优化，我们可以参照[这个知乎上的文章](https://zhuanlan.zhihu.com/p/147366852)，将task分为多层，处理的时候使用shell来执行指令，这样虽然机器忙了，但是我们闲了呀！此文章中还有将运行C++文件设置为快捷键(比如按下F4就执行“运行C/C++文件”的指令)，跟着配置完一遍以后实在是让人心旷神怡。这就等待感兴趣的同学去探索了。

***

[^1]: [来源于CSDN上的一个方法](https://blog.csdn.net/qq_42417071/article/details/137438374)

