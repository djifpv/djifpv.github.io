### 语音包
音频
[rc_audio](./assets/rc_audio.mp3)
文案
```text
飞控解锁
飞控上锁
空中模式
自稳模式
手动模式
反乌龟模式
电池电量不足
信号较弱
信号危险
```
生成命令
```shell
cd assets
mkdir rc_audio
ffmpeg -i ./rc_audio.mp3 -y -ss 00:00:00.000 -t 00:00:01.500 -acodec pcm_s16le -ar 8000 -ac 1 ./rc_audio/armed.wav
ffmpeg -i ./rc_audio.mp3 -y -ss 00:00:01.800 -t 00:00:01.500 -acodec pcm_s16le -ar 8000 -ac 1 ./rc_audio/disarm.wav
ffmpeg -i ./rc_audio.mp3 -y -ss 00:00:03.500 -t 00:00:01.500 -acodec pcm_s16le -ar 8000 -ac 1 ./rc_audio/airmd.wav
ffmpeg -i ./rc_audio.mp3 -y -ss 00:00:05.520 -t 00:00:01.500 -acodec pcm_s16le -ar 8000 -ac 1 ./rc_audio/angmd.wav
ffmpeg -i ./rc_audio.mp3 -y -ss 00:00:06.800 -t 00:00:01.500 -acodec pcm_s16le -ar 8000 -ac 1 ./rc_audio/acro.wav
ffmpeg -i ./rc_audio.mp3 -y -ss 00:00:08.500 -t 00:00:02.000 -acodec pcm_s16le -ar 8000 -ac 1 ./rc_audio/flip.wav
ffmpeg -i ./rc_audio.mp3 -y -ss 00:00:10.500 -t 00:00:02.000 -acodec pcm_s16le -ar 8000 -ac 1 ./rc_audio/lowbat.wav
ffmpeg -i ./rc_audio.mp3 -y -ss 00:00:12.500 -t 00:00:01.500 -acodec pcm_s16le -ar 8000 -ac 1 ./rc_audio/siglow.wav
ffmpeg -i ./rc_audio.mp3 -y -ss 00:00:14.500 -t 00:00:01.500 -acodec pcm_s16le -ar 8000 -ac 1 ./rc_audio/sigctr.wav
```