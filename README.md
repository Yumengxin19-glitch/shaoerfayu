# 法语视频跟读长期版（零维护 Manifest）

这是一个适合长期维护的 GitHub Pages 静态版本。网页程序和课程素材彻底分开：**以后新增、删除或替换视频/字幕/音频，不需要修改 `index.html`，也不需要维护 `audio-manifest.json`。**

## 以后主要只维护 `assets/`

```text
assets/
├── video.mp4                         ← 固定视频文件名
├── subtitles.json                    ← 字幕、时间轴、中文、音标
└── audio/
    ├── sentences/                    ← 句子音频
    │   ├── s001.mp3                  ← 文件名 = subtitles.json 中的句子 id
    │   ├── s002.mp3
    │   └── ...
    │
    └── words/                        ← 单词音频
        ├── bonjour.mp3               ← 文件名 = 单词规范化后的 key
        ├── martin.mp3
        └── ...
```

## 1. 换视频

把新视频命名为：

```text
video.mp4
```

直接覆盖：

```text
assets/video.mp4
```

不用改 HTML。

## 2. 新增/删除/修改句子

只编辑：

```text
assets/subtitles.json
```

每句的 `id` 必须保持唯一，例如：

```json
{
  "id": "s018",
  "start": 132.0,
  "end": 138.0,
  "fr": "Bonjour tout le monde.",
  "zh": "大家好。",
  "ipa": "",
  "speak": "Bonjour tout le monde."
}
```

### 如果这句话有自定义音频

只需要创建：

```text
assets/audio/sentences/s018.mp3
```

网页会自动寻找它。**不需要任何 manifest。**

### 删除一句

删除 `subtitles.json` 中对应句子；如果它有音频，再删除对应的：

```text
assets/audio/sentences/对应的句子ID.mp3
```

## 3. 替换句子音频

保持文件名不变，直接覆盖 MP3。

例如：

```text
assets/audio/sentences/s018.mp3
```

换成新录音，网页自动使用新版。

## 4. 单词音频：不再维护 manifest

单词音频放在：

```text
assets/audio/words/
```

文件名使用“规范化后的单词名”：

- `Martin` → `martin.mp3`
- `bonjour` → `bonjour.mp3`
- `français` → `francais.mp3`
- `l'école` → `l-ecole.mp3`

规则：转小写、去重音符号、标点/空格变成 `-`。

网页在点击单词时才检查对应 MP3，因此**不会因为单词很多而拖慢首次加载**。如果找不到 MP3，就自动使用手机/浏览器的法语 TTS。

## 5. `subtitles.json` 的 version

修改视频、字幕或音频后，建议把：

```json
"version": "20261004-1"
```

改成新的版本号，例如：

```json
"version": "20261005-1"
```

这样可以帮助手机浏览器跳过旧缓存，拿到最新素材。

## 6. 发布到 GitHub Pages

1. 把整个项目文件夹上传到 GitHub。
2. 打开仓库 **Settings → Pages**。
3. 选择 **Deploy from a branch**。
4. Branch 选择 `main`，目录选择 `/ (root)`。
5. 保存，等待 GitHub Pages 发布。

以后更新课程时，通常只需要替换/上传 `assets/`。分享链接保持不变。

## 最重要的一条规则

> **句子音频文件名 = 句子 ID；单词音频文件名 = 规范化后的单词名。**

只要遵守这个规则，就不需要 `audio-manifest.json`。

## 注意

不要双击 `index.html` 测试。网页需要通过 GitHub Pages、Netlify 或本地 HTTP 服务器访问。
