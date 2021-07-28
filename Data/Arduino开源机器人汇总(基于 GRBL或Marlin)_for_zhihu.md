# Arduino开源机器人汇总(基于 GRBL或Marlin)



[toc]



## 概要

[GRBL](https://github.com/grbl/grbl) 是一个开源的嵌入式CNC雕刻机框架， 可以直接在Arduino / STM32这类MCU上运行.  内置标准的GCode解析器,  针对有限的单片机资源做了很多的底层优化，是一个高性能低成本的运动控制方案。 另外，其运动规划框架具有极高的学习价值。 因为代码质量比较高，容易对其进行裁剪/自定义运动学算法, 因此也被广泛的用于其他的开源机器人， 例如画图机器人/机械手臂等等. 

本文将介绍几款经典的基于Arduino运动控制框架的GRBL/Marlin的开源机器人(共10款)，并根据其结构进行分类， 同时也会对我接触过的几款机器人做一下技术方案的介绍。 涉及的机器人结构包括XYZ结构, CoreXY结构， Scara结构.

> 说明 : 课程面列举的资源， 很大一部分来自于国外社区跟视频网站， 为了正常下载跟浏览你需要一点点的超能力。 



## XYZ结构

![image-20210724230936386](image/开源机器人汇总(基于GRBL与Marlin)/image-20210724230936386.png)

XYZ结构广泛的应用于CNC雕刻机/激光雕刻机/切割机/绘图机器人/3D打印机等。 , X轴Y轴Z轴分别用三个滑台/丝杆控制， 三个轴之间相对独立，不发生耦合关系。 优点就是精度高，在进行运动规划的时候，步进的步数跟滑台的位置之间的关系就是简单的线性关系,  不需要频繁做正逆向运动学， 计算量比较小。



在学习阶段，尤其是学习GRBL的使用或者做轨迹规划实验的时候， 建议大家使用绘图机器人来入门。 原因如下：

1. 只需要用两个步进，对结构件刚性要求不高， 便宜. 
2. 安全环保，不像CNC雕刻机会产生非常大噪音。
3. 可以让绘图机器人帮我们写手写作业 / 检查 / 教案。

激光雕刻机也ok，只是激光头会比较贵. 



### DrawBot 绘图机器人



<img src="https://raw.githubusercontent.com/mushroom-x/Markdown4Zhihu/master/Data/Arduino开源机器人汇总(基于 GRBL或Marlin)/image-20210725000729842.jpg" alt="image-20210725000729842" style="zoom:50%;" />



| Tag          | 内容                                                         |

| ------------ | ------------------------------------------------------------ |

| 项目名称     | DrawBot V1.1                                                 |

| 作者         | [henryarnold](https://www.thingiverse.com/henryarnold)   [YouTube](https://www.youtube.com/channel/UCQcu_VWY9kYyM6-QIzB6u0w)  \| MoustafaElkady  [Youtube](https://www.youtube.com/channel/UC50gnFXNgEDQPIr90Hzl7HA) |

| 效果视频     | [How To Make Pen Plotter / Homework Writing Machine at Home](https://www.youtube.com/watch?v=u26Wt8eY5zc) |

| 项目主页     | 无                                                           |

| 运动控制框架 | GRBL                                                         |

| 代码仓库     | [grbl-servo](https://github.com/robottini/grbl-servo)  GRBL的分支，Z轴用舵机控制. |

| 安装教程     | [How To Make DIY Pen Plotter / Homework Writing Machine at Home](https://test3dprints.com/arduino/homework-writing-machine/) |

| 3D模型下载   | [Thingiverse - Drawing Robot - Arduino Uno + CNC Shield + GRBL]([Drawing Robot - Arduino Uno + CNC Shield + GRBL by henryarnold - Thingiverse](https://www.thingiverse.com/thing:2349232)) |


效果视频跟安装教程是另外一个老哥MoustafaElkady做的, 很酷也很燃. 



推荐教程: 

* [写字机器人保姆级教程-Bilibili](https://www.bilibili.com/video/BV1u5411e7GS?p=1)



### DREMEL CNC 三轴雕刻机

3轴的CNC结构

<img src="https://raw.githubusercontent.com/mushroom-x/Markdown4Zhihu/master/Data/Arduino开源机器人汇总(基于 GRBL或Marlin)/image-20210728234644247.jpg" alt="image-20210728234644247" style="zoom:50%;" />

<img src="https://raw.githubusercontent.com/mushroom-x/Markdown4Zhihu/master/Data/Arduino开源机器人汇总(基于 GRBL或Marlin)/image-20210728234707764.jpg" alt="image-20210728234707764" style="zoom:50%;" />



| Tag          | 内容                                                         |

| ------------ | ------------------------------------------------------------ |

| 项目名称     | DREMEL CNC                                                   |

| 作者         | Nikodem Bartnik   [Youtube](https://www.youtube.com/user/nikodembartnik)   [Facebook](https://www.facebook.com/profile.php?id=100063593371467) |

| 效果视频     | [ Fully Open Source DIY CNC Machine - Dremel CNC-Youtube](https://www.youtube.com/watch?v=ps72xPkdDh8) [B站搬运视频](https://www.bilibili.com/video/BV1ev41167cy?from=search&seid=13566530558270723556) |

| 项目主页     | [dremel-cnc](https://indystry.cc/dremel-cnc/)                |

| 运动控制框架 | GRBL                                                         |

| 代码仓库     | [grbl](https://github.com/grbl/grbl)                         |

| 安装教程     | [Instructables - DIY 3D Printed Dremel CNC](https://www.instructables.com/DIY-3D-Printed-Dremel-CNC/) |

| 3D模型下载   | [Instructables - DIY 3D Printed Dremel CNC](https://www.instructables.com/DIY-3D-Printed-Dremel-CNC/) |


作者做的安装视频教程非常详细, 十分感人。使用的就是标准的GRBL固件，需要配置一些参数。 



### INDYMILL 三轴雕刻机

DIY OPEN SOURCE METAL CNC MACHINE 开源金属版CNC雕刻机

跟上面的**DREMEL CNC** 作者是同一个人, 可以理解为升级版， 用全金属打造. 

![image-20210727093350634](image/Arduino开源机器人汇总(基于 GRBL或Marlin)/image-20210727093350634.png)

| Tag          | 内容                                                         |

| ------------ | ------------------------------------------------------------ |

| 项目名称     | INDYMILL                                                     |

| 作者         | Nikodem Bartnik   [Youtube](https://www.youtube.com/user/nikodembartnik)   [Facebook](https://www.facebook.com/profile.php?id=100063593371467) |

| 效果视频     | [IndyMill - Open Source DIY CNC Machine #4 Final Test! - YouTube](https://www.youtube.com/watch?v=5jFCecZdbGs) [B站搬运](https://www.bilibili.com/video/BV1RA411v75T?from=search&seid=14087144026813602452) |

| 项目主页     | [IndyMill – DIY Open Source Metal CNC Machine – Indystry.cc](https://indystry.cc/indymill/) |

| 运动控制框架 | GRBL                                                         |

| 代码仓库     | [grbl](https://github.com/grbl/grbl)                         |

| 安装教程     | 项目主页有安装视频教程,  另外还有配套了40页的PDF安装教程， 不过是付费的 $10 |

| 3D模型下载   | [IndyMill-STL](https://indystry.cc/wp-content/uploads/2021/03/IndyMill-STL.zip) |

| BOM表        | [DIY Dremel CNC parts list - Google Sheets](https://docs.google.com/spreadsheets/d/1kMXrG71ICJv4-k7Ib0bylE4AacfpNgEWceAIhokquVQ/edit#gid=0) |




## CoreXY结构

与传统XYZ结构不同，CoreXY 是一种仅使用一根同步带就可以控制末端在XY两个方向运动的结构，非常巧妙。 

CoreXY结构无论是移动X轴或者是移动Y轴，都需要两个步进电机同时配合运动, 所以是一种并联结构. 

相对于XYZ结构, CoreXY结构相对紧凑，工作空间更大一些。 同时因为CoreXY结构可以令两个两个步进都固定， 所以末端的惯性就小， 可以更快的速度进行运动.



CoreXY结构原理可以学习B站教程[结构详解，hbot和corexy结构的原理和区别-Bilibili](https://www.bilibili.com/video/BV1RJ411a7U2)



### 大鱼DIY写字机器人V2.0 Pro

![image-20210725004406243](image/开源机器人汇总(基于GRBL与Marlin)/image-20210725004406243.png)

| Tag          | 内容                                                         |

| ------------ | ------------------------------------------------------------ |

| 项目名称     | 大鱼DIY写字机器人V2.0 Pro                                    |

| 作者         | 大鱼DIY [Bilibili](https://www.bilibili.com/video/BV1Uh411Q7Zp/?spm_id_from=333.788.b_7265636f5f6c697374.3) |

| 效果视频     | [大鱼DIY写字机器人V2.0 Pro 效果展示](https://www.bilibili.com/video/BV1Uh411Q7Zp/?spm_id_from=333.788.b_7265636f5f6c697374.3) |

| 项目主页     | 无                                                           |

| 运动控制框架 | GRBL                                                         |

| 代码仓库     | [grbl](https://github.com/grbl/grbl) , GRBL内置对CoreXY结构的支持 |

| 安装教程     | [视频-PART2](https://www.bilibili.com/video/BV1Uh411Q7Zp?p=2) [视频-PART3](https://www.bilibili.com/video/BV1Uh411Q7Zp?p=3) |

| 3D模型下载   | 百度网盘链接：https://pan.baidu.com/s/1C6H7iBoDg0USvALdU9V_gw     提取码：DW2P |

| BOM表        | 见网盘文件 `大鱼写字机DayuWriter V2.0 Pro采购清单.xlsx`      |


大鱼DIY的这个视频，在B站上非常火， 在B站上是顶流， 拥有81W的播放量。同时也是做了非常详细的视频教程, 开源精神万岁.



## SCARA结构

关节臂形的结构， 统称为SCARA结构。 也是我目前玩的最多的机械臂的机型。

![image-20210725030958645](image/开源机器人汇总(基于GRBL与Marlin)/image-20210725030958645.png)

上图的机器人，使用的主控板几乎清一色的都是Mega2560.

为什么做SCARA机械臂不用Arduino Uno呢？ 我之前开发grbl版本的DArm就踩过雷。

1. GRBL项目几乎是压榨干了UNO所有的性能跟内存资源了， 强行将SCARA机械臂的逻辑添加进去, Uno资源会不够用， 而内存处于临界值的时候，及其容易产生莫名其妙的错误. 
2. Uno硬件资源太少， 不方便扩展第四轴， 或者拓展其他的传感器. 





### 20sffactory 机械臂

![image-20210725030413423](image/开源机器人汇总(基于GRBL与Marlin)/image-20210725030413423.png)



![image-20210725030135154](image/开源机器人汇总(基于GRBL与Marlin)/image-20210725030135154.png)

| Tag                 | 内容                                                         |

| ------------------- | ------------------------------------------------------------ |

| 项目名称            | 20sffactory Arm                                              |

| 作者                | 20sffactory   [Facebook](https://www.facebook.com/20sffactory) [Youtube](https://www.youtube.com/channel/UC4LSwwclUZ7gCLbgWvXnWLg) |

| 效果视频            | [20sffactory 3D打印机械臂-视频合集- Bilibili视频搬运](https://www.bilibili.com/video/BV16V411p7AZ) |

| 项目主页            | [ 20sffactory](https://www.20sffactory.com/robot/about)      |

| 运动控制框架        | Marlin 2.0                                                   |

| 代码仓库            | [20sffactory/community_robot_arm](https://github.com/20sffactory/community_robot_arm)  [Marlin 2.0 Guide](https://www.20sffactory.com/robot/resource/marlin) |

| 资源列表            | [Resource -20sffactory](https://www.20sffactory.com/robot/resource) |

| 3D模型下载+安装教程 | [Resource-20sffactory](https://www.20sffactory.com/robot/resource#assembly) , 代码仓库里有CAD Files |

| BOM表               | [BOM表](https://www.20sffactory.com/robot/resource#BOM)      |


这款机械臂作者没有给他起名字，用作者的名字来命名.  目前为止，生态最好，做的最完善的一款。 如果你想玩机械臂的话， 就从这款机械臂开始玩吧。  作者的设计是基于ftobler设计的版本做的改进， [RobotArm by ftobler - Thingiverse ](https://www.thingiverse.com/thing:1718984)   旧版的图片如下: 

<img src="https://raw.githubusercontent.com/mushroom-x/Markdown4Zhihu/master/Data/Arduino开源机器人汇总(基于 GRBL或Marlin)/image-20210725024239104.png" alt="image-20210725024239104" style="zoom: 50%;" />



在原来的基础上，做了机械结构的改进， 改为同步带传动, 加上了第四轴， 同时也做了大量的内容生态, 同时现在仍然生机勃勃.  机械臂基于Marlin 2.0做的配置修改， 内置运动学算法。 做的比较完善。  从效果视频来看， 高速运动的时候，机械臂仍然可以保持稳定, 可以

说非常赞了.   







### DArm 机械臂

![image-20210728233736389](image/Arduino开源机器人汇总(基于 GRBL或Marlin)/image-20210728233736389.png)

| Tag          | 内容                                                         |

| ------------ | ------------------------------------------------------------ |

| 项目名称     | DArm                                                         |

| 作者         | 廖洽源 Liao Qiayuan  [知乎](https://www.zhihu.com/people/liao-qia-yuan) |

| 效果视频     | [3D Print Desktop Robot Arm Drawing test(DARM)](https://www.youtube.com/watch?v=TB_bw-uhI8M) |

| 项目主页     | [A 3D Printing desktop arm that can write and draw!!!](https://hackaday.io/project/28264-darm) |

| 运动控制框架 | Marlin 2.0                                                   |

| 代码仓库     | [DArm - Github](https://github.com/QiayuanLiao/DArm)         |

| SW工程       | 见*代码仓库*, 作者把Solidworks的工程放到里面了.              |

| 3D模型下载   | [3d print desktop robot arm(DARM) - thingiverse](https://www.thingiverse.com/thing:1204552) |

| BOM表        | 见*3D模型下载*                                               |

| 安装教程     | [【教程】桌面机械臂DARM 制作教程  - 百度贴吧](https://tieba.baidu.com/p/4228025116?red_tag=0378953567) |


DArm是15年的一个开源项目, 作者是廖洽源 Liao Qiayuan , 毕业于广东工业大学 机械电子工程。 

 我在19年跟Sipeed合作的时候，也写过GRBL版本的DArm固件， 我的好朋友小峰也帮我优化过它的结构。 机械臂的臂展比较大， 连杆使用了圆柱管材， 减少了3D打印的部分， 成本比较低.  但是这种圆形管材的设计也会导致连接件易松动，进而影响连杆长度参数， 末端也会产生一定程度的歪斜,  难以保证末端的精度。同时对装配的要求也会比较高。  亮点是作者提供了开源的Solidworks工程， 大家如果要复现的话，可以把圆柱杆替换为板材。总体来讲，如果对工作区要求不高的话，建议玩**20sffactory 机械臂**。 



### Drawbot 机械臂

| Tag          | 内容                                                         |

| ------------ | ------------------------------------------------------------ |

| 项目名称     | DArm                                                         |

| 作者         | 张明 @成都 [youtube](https://www.youtube.com/channel/UCOA4N2TRip56QAWK2ay6bfQ) |

| 效果视频     | [drawbot repetition precision test - YouTube](https://www.youtube.com/watch?v=NTBxLTUPyTU) |

| 项目主页     | [drawbot by MG-dream-technology - Thingiverse](https://www.thingiverse.com/thing:3096135) |

| 运动控制框架 | Marlin 2.0                                                   |

| 代码仓库     | 没开源                                                       |

| 3D模型下载   | [drawbot by MG-dream-technology - Thingiverse](https://www.thingiverse.com/thing:3096135) |

| BOM表        | 见*安装教程*                                                 |


Drawbot的项目是18年做的，整体结构参考了DArm， 将其转换为2自由度的平面绘图机器人, 之前在Arduino中文社区里大火. 

Scara结构的绘图机器人， 因为机型自身的原因，精度没XYZ或者CoreXY结构的绘图机器人高，而且XYZ结构要更简单一些。 如果是研究的话，可以用来学习, 不过作者好像并没有开源源码。其实原理不难，比DArm还要简单一点点。    

好在我的好朋友小峰做了一版金属版本的Drawbot， 并且开源了**GRBL-stm32版本**的SCARA绘图机器人的固件. [Uniquemf/grbl-stm32-scara (github.com)](https://github.com/Uniquemf/grbl-stm32-scara) , 这个也是他本科的毕业设计。

<img src="https://raw.githubusercontent.com/mushroom-x/Markdown4Zhihu/master/Data/Arduino开源机器人汇总(基于 GRBL或Marlin)/image-20210725114259197.png" alt="image-20210725114259197" style="zoom:50%;" />



### UArm Swift Pro  机械臂

![image-20210728234130361](image/Arduino开源机器人汇总(基于 GRBL或Marlin)/image-20210728234130361.png)

| Tag          | 内容                                                         |

| ------------ | ------------------------------------------------------------ |

| 项目名称     | UArm Swift Pro                                               |

| 作者         | ufactory                                                     |

| 效果视频     | [uArm Swift Pro Robotic Arm Review: Professional Kit for Educators]([uArm Swift Pro Robotic Arm Review: Professional Kit for Educators - YouTube](https://www.youtube.com/watch?v=HsqwghvthKs)) |

| 项目主页     | [uArm – store.ufactory.cc](https://www.ufactory.cc/pages/uarm) |

| 运动控制框架 | GRBL-Mega / Marlin                                           |

| 代码仓库     | [SwiftProForArduino](https://github.com/uArm-Developer/SwiftProForArduino) |

| 3D模型下载   | 金属件，结构不开源                                           |


之前买过一个UArm Swift Pro， 这款机械臂全金属机身， 做工不错.  旧版的UArm Swift Pro固件是基于Marlin做的. 

但是UArm Swift Pro最新的固件V4.9.0以后，使用的都是基于GRBL改的固件版本。 因为Marlin是针对3D打印机设计的固件， 对于这种关节臂型的机械臂来讲，就显得很庞大. GRBL小巧，更容易学习， 也更容易定制.

看源码的时候，注意选择分支版本号`V4.0`. 

![image-20210725143502834](image/Arduino开源机器人汇总(基于 GRBL或Marlin)/image-20210725143502834.png)

UArm Swift Pro 主控使用的主控是 Mega2560.   步进电机驱动使用了三个LV8729跟一个A4988 。



<img src="https://raw.githubusercontent.com/mushroom-x/Markdown4Zhihu/master/Data/Arduino开源机器人汇总(基于 GRBL或Marlin)/image-20210725144309983.jpg" style="zoom:33%;" />



<img src="https://raw.githubusercontent.com/mushroom-x/Markdown4Zhihu/master/Data/Arduino开源机器人汇总(基于 GRBL或Marlin)/image-20210725150110935.jpg" alt="image-20210725150110935" style="zoom: 33%;" />

UArm方案， 比较有亮点的地方是， 将步进电机+减速齿轮 + 霍尔IC编码器AS5600 (I2C接口)做到了一起， 磁铁是粘贴到减速齿的轴上的.   这样在机械臂上电的时候，主控就可以知道机械臂各个关节的绝对位置了， 所以UArm没有Homing的过程.  这样做的另外一个好处就是， UArm可以给步进电机卸力， 然后通过实时的采集编码器的角度信息， 完成拖动示教。 大家如果用步进电机+减速同步带的方案的时候， 也可以参考类似的做法， 在减速输出轴的位置添加磁铁跟霍尔IC编码器. 

<img src="https://raw.githubusercontent.com/mushroom-x/Markdown4Zhihu/master/Data/Arduino开源机器人汇总(基于 GRBL或Marlin)/image-20210726102230362.png" alt="image-20210726102230362" style="zoom:50%;" />



<img src="https://raw.githubusercontent.com/mushroom-x/Markdown4Zhihu/master/Data/Arduino开源机器人汇总(基于 GRBL或Marlin)/QQ图片20210426032625.jpg" alt="QQ图片20210426032625" style="zoom:25%;" />

<img src="https://raw.githubusercontent.com/mushroom-x/Markdown4Zhihu/master/Data/Arduino开源机器人汇总(基于 GRBL或Marlin)/image-20210725144001806.jpg" alt="image-20210725144001806" style="zoom: 25%;" />

但是严格意义上来讲， UArm的步进电机方案，并不能称得上真正意义上的**闭环步进**.   在运行过程中，主控不会主动的去查询更新当前编码器的角度，如果步进电机在运动过程中产生了丢步的情况, 不会做任何的补偿/处理， AS5600霍尔IC编码器的用途只出现在Homing的时候。

还有顺带说一下UArm Swift Pro 末端的旋转关节舵机, 末端旋转关节配置的舵机规格跟MG90s差不多， 扭力很小， 只不过是四线舵机， 应该是多了一个电位计的ADC信号线， 但是固件里面并没有用到这个ADC采样线，普通PWM舵机也可以用在上面.

### Mirobot 六自由度机械臂

<img src="https://raw.githubusercontent.com/mushroom-x/Markdown4Zhihu/master/Data/Arduino开源机器人汇总(基于 GRBL或Marlin)/image-20210728234224169.png" alt="image-20210728234224169" style="zoom:50%;" />

| Tag          | 内容                                                         |

| ------------ | ------------------------------------------------------------ |

| 项目名称     | Mirobot                                                      |

| 作者         | 周冬旭 中国矿业大学 博士  [藏起来 - 知乎 (zhihu.com)](https://www.zhihu.com/people/cang-qi-lai-20) |

| 效果视频     | [机械臂五子棋人机对弈-AlphaZero强化学习+Mirobot六自由度机械臂](https://www.bilibili.com/video/BV1PT4y1A7cX) |

| 项目主页     | [wlkata-mirobot]([Home WLKATA \| 6-Axis Mini Robot Arm for Education](https://www.wlkata.com/)) |

| 运动控制框架 | GRBL-Mega                                                    |

| 代码仓库     | 固件不开源,    [Wlkata Mirobot Supporters Forum (github.com)](https://github.com/wlkata) |

| 3D模型下载   | 不开源，注塑件 。  开源了可用于搭建URDF模型的STL文件 [wlkata/Mirobot-STL: STL (github.com)](https://github.com/wlkata/Mirobot-STL) |


之前跟Mirobot有过机械臂案例的项目合作， 所以跟周冬旭 周博有过交流。 之前我修改过的Mirobot Python SDK [wlkata/mirobot-py: WLkata Mirobot Python SDK (github.com)](https://github.com/wlkata/mirobot-py), 被周博fork到官方代码仓库里了， 非常荣幸.  

GRBL在底层设计里面，并没有考虑到末端姿态欧拉角的问题，只局限于末端的三维坐标 [x,y,z].  而Mirobot开源的6自由度机械手臂的固件里面有6DoF机械臂的正逆向运动学， 有比较好的学习价值。固件在最初发布的时候是开源的， 不过现在固件不开源了。 



### MK2 Plus 机械臂

<img src="https://raw.githubusercontent.com/mushroom-x/Markdown4Zhihu/master/Data/Arduino开源机器人汇总(基于 GRBL或Marlin)/image-20210728234257269.png" alt="image-20210728234257269" style="zoom:50%;" />





| Tag          | 内容                                                         |

| ------------ | ------------------------------------------------------------ |

| 项目名称     | MK2 Plus 机械臂                                              |

| 作者         | [Jacky Le](https://www.thingiverse.com/jackyltle)   [YouTube](https://www.youtube.com/channel/UCETakZeJ0g3TAj7vm5zGJ7Q) |

| 效果视频     | [Cheap 3D printed Robot Arm Free Source code - Part 3 - YouTube](https://www.youtube.com/watch?v=m-svr2s2QuY&t=5s) |

| 项目主页     | 无                                                           |

| 运动控制框架 | GRBL                                                         |

| 代码仓库     | [grbl-servo](https://github.com/robottini/grbl-servo)  GRBL的分支，Z轴用舵机控制. |

| 安装教程     | [Robot Arm MK2 Plus (Stepper Motor Used) : 11 Steps - Instructables](https://www.instructables.com/Robot-Arm-MK2-Plus-Stepper-Motor-Used/) |

| 3D模型下载   | 见安装教程                                                   |

| BOM表        | 见安装教程                                                   |




MK1机械臂跟MK2机械臂都是基于舵机来做的, 作者是EEZYrobots, [EEZYrobots官网](http://www.eezyrobots.it/)

MK系列的机械臂玩的人比较多， 之前我基于MK1机械臂写过机械臂运动学的课程  [机械臂运动学控制及Python实现-1Z实验室-网易云课堂](https://study.163.com/course/introduction/1006457010.htm?share=2&shareId=400000000650020) 

<img src="https://raw.githubusercontent.com/mushroom-x/Markdown4Zhihu/master/Data/Arduino开源机器人汇总(基于 GRBL或Marlin)/image-20210725005758796.jpg" alt="image-20210725005758796" style="zoom:50%;" />

MK2 Plus版本是由[Jacky Le](https://www.thingiverse.com/jackyltle)  设计制作的， 用步进电机替换了舵机. 

![image-20210728234343239](image/Arduino开源机器人汇总(基于 GRBL或Marlin)/image-20210728234343239.png)

其设计原型为ABB IRB460机械臂。 

**没有深入针对当前的机型去定制GRBL的固件，使用的是标准的GRBL固件， 使用方式仅局限于示教. **

也有一个不依赖GRBL版本的，但是也没有运动学的部分.  参考教程[MK2 Plus Robot Arm Controller](https://create.arduino.cc/projecthub/yasaspeiris/mk2-plus-robot-arm-controller-458d55)

