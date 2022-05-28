### ELRS改启动音乐流程
1. 找一段RTTTL格式的音乐, 可以在[这里](https://adamonsoon.github.io/rtttl-play/)试听
```
# 例子音乐
Mozart:d=16,o=5,b=125:16d#,c#,c,c#,8e,8p,f#,e,d#,e,8g#,8p,a,g#,g,g#,d#6,c#6,c6,c#6,d#6,c#6,c6,c#6,4e6,8c#6,8e6,32b,32c#6,d#6,8c#6,8b,8c#6,32b,32c#6,d#6,8c#6,8b,8c#6,32b,32c#6,d#6,8c#6,8b,8a#,4g#,d#,32c#,c,c#,8e,8p,f#,e,d#,e,8g#,8p,a,g#,g,g#,d#6,c#6,c6,c#6,d#6,c#6,c6,c#6,4e6,8c#6,8e6,32b,32c#6,d#6,8c#6,8b,8c#6,32b,32c#6,d#6,8c#6,8b,8c#6,32b,32c#6,d#6,8c#6,8b,8a#,4g#
```
2. 在ExpressLRS项目目录下, 执行
```bash
python3 -i src/python/melodyparser.py # 他将加载melodyparser模块, 并同时启动命令行交互界面
rtttl = '....' # RTTTL格式音乐, 复制过来
parse(rtttl) # 将生成RTTTL解析后的播放序列, 这是一段C语言数组代码, 复制这段代码
```
3. 在项目文件中全局搜索
```C
#if defined(MY_STARTUP_MELODY_ARR)
```
会找到类似代码, 这是C语言编写的开机旋律, 默认是有一段旋律的, 直接改他的.
```C
#if defined(MY_STARTUP_MELODY_ARR)
// It's silly but I couldn't help myself. See: BLHeli32 startup tones.
static const uint16_t melody[][2] = MY_STARTUP_MELODY_ARR;
#elif defined(JUST_BEEP_ONCE)
static const uint16_t melody[][2] = ... ;
#else
static const uint16_t melody[][2] = ... ;// 这里是默认的播放音频序列, 是超级玛丽游戏的声音. 把他改成2中Python生成的播放序列代码.
#endif
```
进行修改,并保存.

因为```MY_STARTUP_MELODY_ARR``` 这个宏定义如果被定义会导致编译(系统m1 macOS)不通过(链接时报符号重定义异常), 所以不能通过定义该宏来自定义声音, 这是ELRS源码的一个BUG. 所以必须改源代码来实现自定义声音.

4. 编译固件并安装. 如果之前安装过bootloader不需要重复安装.