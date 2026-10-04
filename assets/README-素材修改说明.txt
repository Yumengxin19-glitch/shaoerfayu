【零维护 Manifest 版素材修改说明】

以后不需要维护 audio-manifest.json。这个版本会按照固定文件名自动寻找音频。

一、视频
1. 新视频命名为 video.mp4
2. 覆盖 assets/video.mp4

二、字幕
编辑 assets/subtitles.json。
- id：每句唯一的身份证，新增句子时必须唯一
- start / end：时间轴（秒）
- fr：法语
- zh：中文
- ipa：音标
- speak：跟读文本

三、句子音频
句子音频放在：
assets/audio/sentences/

规则：文件名必须等于字幕里的 id。
例如字幕：
  "id": "s018"
就把音频命名为：
  assets/audio/sentences/s018.mp3

新增句子音频：直接新增同名 mp3。
删除句子：删除字幕中的句子，并删除对应 mp3。
替换音频：直接覆盖同名 mp3。

四、单词音频
单词音频放在：
assets/audio/words/

网页会自动把单词转换成文件 key：
- Martin → martin.mp3
- français → francais.mp3
- l'école → l-ecole.mp3

规则：小写 + 去重音符号 + 标点/空格转成 -。

单词音频只在点击单词时检查，不会阻塞首次加载。找不到文件时自动使用法语 TTS。

五、更新版本号
修改素材后，建议修改 subtitles.json 顶部的 version，例如：
20261004-1 → 20261005-1
这样手机更容易拿到最新缓存。

六、上传 GitHub
直接上传整个项目，或者只把更新后的 assets 文件覆盖到 GitHub。index.html 不需要重新生成。
