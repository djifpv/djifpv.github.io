# [Tinyhawk2](https://emax-usa.com/products/tinyhawk2)
空心杯,可室内飞行
[手册](./assets/Tinyhawk%20II%20Freestyle%20BNF%20Instruction%20Manual%20v1.5.pdf)

* 有个机载小摄像头.
* 送了两块电池(1s450mah, 2s300mah), 一块能飞三分钟.
* 充电板用于给电池充电.

### 飞前准备
---
视频 [「FPV穿越机」银燕Tinyhawk2新手教程（飞前准备篇）](https://www.bilibili.com/video/BV1GT4y1L75Z)

### 使用[Betaflight](https://github.com/betaflight/betaflight-configurator)设置飞机
---
视频 **必从头到尾看, 详细介绍软件** [【穿越机FPV】新飞机起飞前Betaflight设置和不能解锁与飞行不正常问题排除探讨](https://www.bilibili.com/video/BV137411b7G3/)

文章 [Frsky 2019款 X9D plus se与Tinyhawk2的对频](https://www.bilibili.com/read/cv7127727)

文章 ISRM固件2.1.6无法对频问题 [睿斯凯 x9d plus se 2019 与tinyhawk s 2 对频问题](https://www.bilibili.com/read/cv10389880)

视频 [[fpv穿越机]Mobula6与新款睿思凯遥控器使用D16协议无法对频？试试这种方法。](https://www.bilibili.com/video/BV1bV411h7vb)

##### 此处需要刷固件
只有1.1.3版本的ISRM固件可以通过ACCST D16连接上飞机, 更新的固件版本无法对频成功, 所以需要刷固件.

从睿思凯官网下载[1.1.3版本的ISRM固件](https://www.frsky-rc.com/wp-content/uploads/Downloads/Firmware/X9DP2019/FW-X9DP2019-ISRM-V1.1.3.zip).

[2.1.6版本的ISRM固件](https://www.frsky-rc.com/wp-content/uploads/Downloads/Firmware/ACCESS-2.x.x/FW-X9DP2019-ISRM-v2.1.6.zip)做个备份, 可以随时刷回来.
```
刷固件流程:
1. TF卡格式化成FAT格式, 将固件文件下载解压放入, 从遥控器电池盖后装入TF卡.
2. 进遥控长按Menu, 然后短按Page切换到TF卡. 选择固件文件, 选择Flash Internal Module.
3. 等待进度条走完, 即完成刷固件.
```

##### 对频
使用betaflight, 连接设备. (插口在摄像头后颈处)
连接上betaflight后:
1. 配置-接收机:
SPI总线接口接收机协议 设置为FRSKY_X
1. 打开CLI
```bash
bind_rx # 对于4.1.x固件
bind_rx_spi # 对于4.0.x固件
```
成功的话，飞机上的蓝色对频灯会常亮。
2. 在遥控对频里 Receiver No栏中选择 `Bind`, 此时遥控器会鸣叫. `Bind`前面有个编号.
3. 在CLI中执行
```bash
set frsky_x_rx_num
```
如果对频成功, 则显示的编号和`Bind`前面显示的编号一致, 此时执行:
```bash
save
```
保存.

### 设置PID
在betaflight软件中选择PID设置.
配置文件1和Rate配置1对应1s 450mah电池
配置文件2和Rate配置2对应2s 300mah电池

### 设置模式
在betaflight软件中选择模式, 并指定通道. 通过遥控器拨杆触发通道来激活模式.
ARM(武装,备战; 打开…的保险) 栏对应电机解锁
FLIP OVER AFTER CRASH对应反乌龟模式, 掉落翻转后可以通过操作来自动翻转
ANGLE(角度模式或称自稳模式) HEADFREE(第三人称) HORIZON(半自稳模式)等为飞行模式, 如果不设置则为ARCO(全手动)模式
```
反乌龟操作: 先锁电机, 开启反乌龟模式, 再解锁电机, 进行操作.
```
**需在遥控器Menu中的MIXES选项卡中配置拨杆对应通道, 才能通过拨杆触发对应模式**

### 飞行
---
1. 拨杆开ARM(通过拨杆触发通道, 触发模式中设置的AUX1对应的ARM)
2. 加油门起飞

降落时关油门关ARM.

### 飞机配置[备份](./assets/BTFL_backup_TinyHawk_II.json)