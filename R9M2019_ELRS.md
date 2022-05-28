### [R9M2019](https://www.frsky-rc.com/product/r9m-2019/)
### [ExpressLRS](./ExpressLRS.md)

### 资料
[【ELRS保姆教程】还能学不会？睿思凯R9系统刷写ELRS，让R9m系统脱胎换骨](https://www.bilibili.com/video/BV15v411P7m3)

### 构建并安装固件
1. 先用ExpressLRS-Configurator工具导入本地下载的固件源码ExpressLRS. 选择符合高频头的选项进行构建.
2. 开始构建后等一段时间, 成功后会生成一个扩展名为.elrs的文件. 把这个elrs文件和```ExpressLRS/src/bootloader/r9mm_elrs_bl.frk```(给接收机刷, 只刷高频头时用不到), ```ExpressLRS/src/bootloader/r9m_elrs_bl.frk```(给高频头刷)拷到遥控器的存储卡里. 还要另外拷贝 ```ExpressLRS/src/lua/elrsV2.lua```到遥控器存储卡的```SCRIPTS/TOOLS```目录.
3. 进遥控器的选项, 找到存储卡里那个r9m_*.flk文件, 刷给高频头固件, 刷好后再把elrs文件刷给高频头.
4. 启用高频头时在Model里把外置高频头协议改成``CRSF``, 高频头开始工作时会发出超级玛丽游戏的那个声音. [改启动声音流程](./R9M2019_Voice.md)

**给接收机刷ELRS固件是另一套流程**
