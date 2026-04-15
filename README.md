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

模板采用严格模式：**字体栈不做降级**，缺字体直接编译报 warning 并在 PDF 中用 `.notdef` 字形占位。请自行将字体放入 `fonts/` 目录。

必需的字体 family（与 macOS 系统字体名保持一致）：

| family name | 用途 | Regular + Bold |
|---|---|---|
| `Times New Roman` | 西文 | ✅ 必需 |
| `Songti SC` | 正文宋体 | ✅ 必需 |
| `Heiti SC` | 标题黑体 | ✅ 必需 |
| `Kaiti SC` | 封面/题目楷体 | ✅ 必需 |

> 字体通过 OpenType **name 表**里的 Family Name 索引，文件名无所谓；若下载的开源字体 family name 不同（如 Noto Serif SC），需要修改 `whu-thesis.typ` 中对应的 `font: (...)` 字段。

### 本地编译

macOS 系统自带以上所有字体，直接：

```bash
typst compile main.typ
```

### Typst 网页端

把你下载的字体文件（.ttf / .otf）放到 `fonts/` 目录，整个项目上传 <https://typst.app> 即可。也可以用 `--font-path fonts`：

```bash
typst compile --font-path fonts main.typ
```

开源替代建议：
- 宋体 → [Noto Serif SC](https://github.com/notofonts/noto-cjk) / [思源宋体](https://github.com/adobe-fonts/source-han-serif)
- 黑体 → [Noto Sans SC](https://github.com/notofonts/noto-cjk) / [思源黑体](https://github.com/adobe-fonts/source-han-sans)
- 楷体 → [LXGW WenKai](https://github.com/lxgw/LxgwWenKai) / [霞鹜文楷](https://github.com/lxgw/LxgwWenKai)

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
