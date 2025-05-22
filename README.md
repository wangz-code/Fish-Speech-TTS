## fish-tts

初步计划作为阅读的 tts 引擎试试, 克隆音色不是很完美但已经达到基本能用的地步

此刻旁边是我花了￥ 350 块从哥布林手中拯救过来的矿卡, 她甚至没有 FP16, 必须给她"铐上"" --half 才能让她(cmp40hx)跟他(fish)跑在 FP32 上, 他未经我的同意下强行占用她大概2G显存但他一定不知道其实她有8G那么大的显存, 即使多来几个他一起上也无所谓。

感觉推她的速度还行, 推的次数太多以至于每秒多少token已经记不清了, 隐隐记得她身上的风扇在他和他们的作用下并没有发出啸叫, 😄歪嘴笑~ 看样子是我的给她新换上的小日子进口的轴承起了作用, 即使 fish 用尽全力确依旧没有把她的显存占满。

等到夏天的时候我给她拂去头发上的灰尘,在她的心脏上贴上我斥巨资买的相变片, 相信她们一定能推的更加卖力。

## 前端运行

```sh
# 开发工具
npm install vite -g

# 开发测试
npm install
npm run dev

--------------

# node 直接部署或使用pm2 start preview.js
node preview.js
```

## 音频样本采集

```sh
# 1.各大视频平台找到媒体使用 yt-dlp下载, 提取比较好的样本截取 90 秒转成wav (fishtts貌似最多限制90秒)
# mp4文件 从第三秒开始(-ss 00:00:03) 时长(-t 90)秒 移除视频流(-vn) 音频采样率(-ar 16000) 声道(-ac 1) 单声道体积会小一些
ffmpeg -i input.mp4 -ss 00:00:03 -t 90 -vn -ar 16000 -ac 1 audio.wav

# 2.使用spleeter模型分离人声和伴奏 https://github.com/deezer/spleeter
separate -p spleeter:2stems -o output audio.wav

# 3.使用distil-whisper模型将音频转成文字, 再使用豆包修正错别字 放在fish-tts/references目录下
https://huggingface.co/BELLE-2/Belle-whisper-large-v3-turbo-zh

# 铛铛铛 完成
```

## ![detail.png](https://raw.githubusercontent.com/wangz-code/fish-tts/main/pp.png)

## 基于

https://github.com/fishaudio/fish-speech
https://github.com/deezer/spleeter
https://huggingface.co/BELLE-2/Belle-whisper-large-v3-turbo-zh
