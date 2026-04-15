# WHU Thesis Typst

武汉大学学位论文 Typst 模板 / Wuhan University Thesis Template for Typst

## 功能特性

- 支持本科（bachelor）、硕士（master）、博士（doctor）学位论文
- 支持学术型（academic）和专业型（professional）学位
- 符合武汉大学学位论文排版规范
- 内置封面、摘要、目录、正文、参考文献、致谢等页面模板
- 支持数学公式、图表、脚注、定理环境等学术写作常用功能

## 快速开始

1. 安装 [Typst](https://typst.app/)
2. 克隆本仓库：

```bash
git clone git@github.com:ZhenyuZhang-sys/whu-thesis-typst.git
```

3. 编辑 `main.typ`，填写论文信息并撰写内容
4. 编译：

```bash
typst compile --font-path fonts main.typ
```

## 字体要求

模板采用严格模式：**字体栈不做降级**，缺字体直接编译报 warning。本模板与 Word 论文模板的字体配置一致，要求以下字体：

| family name | 角色 | 用途 | 文件 |
|---|---|---|---|
| `Source Han Serif` | 思源宋体 | 正文、图标题 | `SourceHanSerifCN-Regular/Bold.otf`（子集化）|
| `Source Han Sans SC` | 思源黑体 | 表标题、章节标题 | `SourceHanSansSC-Regular/Bold.ttf`（子集化）|
| `KaiTi` | 楷体 | 论文题目、引用 | `simkai.ttf`（系统/Word 自带）|
| `FangSong` | 仿宋 | 备用中文 | `simfang.ttf`（系统/Word 自带）|
| `Times New Roman` | 西文衬线 | 西文正文 | `TIMES.TTF` + `TIMESBD/I/BI.TTF` |
| `Arial` | 西文无衬线（黑体配对） | 西文标题 | `ARIAL.TTF` + 多款变体 |

> 中文主字体已迁移至 Adobe **思源宋体 / 思源黑体** 子集化版本（仅 1～2 MB，仓库友好）。子集化字体含 GB2312 + 常用扩展字符；如有生僻字渲染需求，可换为完整版 `SourceHanSerifSC-*.otf` / `SourceHanSansSC-*.otf` 并将 typ 中 `Source Han Serif` 改为 `Source Han Serif SC`。

### 在线获取字体（推荐）

字体包来自 [chillcicada/tntt](https://github.com/chillcicada/tntt) 的 `fonts.zip` 发布（TnTT 是清华大学 Typst 论文模板）。

一行命令下载并解压到 `fonts/` 目录（macOS / Linux）：

```bash
mkdir -p fonts && \
  curl -L -o /tmp/fonts.zip https://github.com/chillcicada/tntt/releases/latest/download/fonts.zip && \
  unzip -o /tmp/fonts.zip -d fonts/
```

Windows PowerShell：

```powershell
New-Item -ItemType Directory -Force fonts | Out-Null
Invoke-WebRequest -Uri "https://github.com/chillcicada/tntt/releases/latest/download/fonts.zip" -OutFile "$env:TEMP\fonts.zip"
Expand-Archive -Force "$env:TEMP\fonts.zip" -DestinationPath fonts
```

下载完成后用 `--font-path fonts` 编译即可（见下文）。

### 编译

```bash
typst compile --font-path fonts main.typ
```

或严格只用仓库内字体、忽略系统字体（推荐；避免跨平台字体名差异）：

```bash
typst compile --font-path fonts --ignore-system-fonts main.typ
```

### Typst 网页端

直接上传整个项目到 <https://typst.app>，`fonts/` 里的字体会被自动识别（请勿上传压缩包）。

### 自定义字体

若要替换 family（比如 macOS 用户想用 `Songti SC`、`Heiti SC`），把字体文件放入 `fonts/`，然后把 `whu-thesis.typ` 里出现的 family 名替换掉。字体通过 OpenType name 表的 Family Name 索引，文件名无所谓。

## 中文粗体（伪粗体）

思源宋体（Source Han Serif）的 Bold 字重渲染较细，模板使用 [cuti](https://typst.app/universe/package/cuti) 提供的描边式伪粗体（仿 MS Word 风格）增强视觉效果。**仅对宋体启用伪粗体**——黑体/楷体/仿宋本身已有真粗体或不需加粗，避免叠加描边导致字形发糊：

```typst
#import "@preview/cuti:0.2.1": fakebold

#show strong: it => context {
  let stack = if type(text.font) == array { text.font } else { (text.font,) }
  if "Source Han Sans SC" in stack or "KaiTi" in stack or "FangSong" in stack {
    it
  } else {
    fakebold(it)
  }
}
```

正文中直接使用 `*加粗内容*` 即可。首次编译需联网下载 `cuti` 包。

详细说明参考：<https://guide.typst.dev/FAQ/chinese-bold>

## 项目结构

```
.
├── main.typ          # 主文件（论文入口）
├── whu-thesis.typ    # 模板核心文件
├── logo/             # 校徽等图片资源
├── fonts/            # 打包的中文字体（Noto CJK + LXGW WenKai）
├── ref/              # BibTeX 参考文献（*.bib）
└── demo.pdf          # 示例输出
```

## 参考文献

参考文献放在 `ref/` 目录下（如 `ref/refs.bib`），使用标准 BibTeX 格式。在 `main.typ` 中调用：

```typst
#make-bibliography("ref/refs.bib")
```

模板使用 `gb-7714-2005-numeric` 国标编号样式（硕博默认 `gb-7714-2005`）。

在正文中引用：

```typst
如 Shannon @shannon_mathematical_1948 所述……
FUSE 的性能问题在 @vangoor_fuse_2017 中已有分析。
```

只有被 `@key` 引用过的条目才会出现在最终的参考文献列表中，未引用的条目自动忽略，bib 可以当作"候选文献池"使用。

示例 bib 见 [`ref/refs.bib`](ref/refs.bib)：

```bibtex
@inproceedings{vangoor_fuse_2017,
  title     = {To FUSE or Not to FUSE: Performance of User-Space File Systems},
  author    = {Vangoor, Bharath Kumar Reddy and Tarasov, Vasily and Zadok, Erez},
  booktitle = {15th USENIX Conference on File and Storage Technologies (FAST 17)},
  year      = {2017},
  url       = {https://www.usenix.org/conference/fast17/technical-sessions/presentation/vangoor},
}
```

带 `url` 字段的条目会在参考文献列表中生成可点击链接，建议为网络资源加上。

## 论文类型配置

在 `main.typ` 中修改 `thesis-type` 和 `degree-class` 参数：

```typst
#show: whu-thesis.with(
  thesis-type: "master",      // bachelor, master, doctor
  degree-class: "academic",   // academic, professional
  // ...其他参数
)
```

## 致谢

感谢 [mgt/whu-thesis](https://github.com/mgt/whu-thesis) LaTeX 模板提供的排版参考。

## License

MIT
