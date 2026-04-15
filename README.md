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

## 在 Typst 网页端使用

Typst 官方网页编辑器（<https://typst.app>）不预装中文字体，本仓库已在 `fonts/` 目录打包了必需的开源字体，上传整个项目即可直接编译，无需额外配置。

字体列表：

| 字体名 | 用途 | 来源 |
|---|---|---|
| Noto Serif SC (Regular / Bold) | 宋体替代 | [notofonts/noto-cjk](https://github.com/notofonts/noto-cjk) |
| Noto Sans SC (Regular / Bold)  | 黑体替代 | 同上 |
| LXGW WenKai (Regular / Bold)   | 楷体替代 | [lxgw/LxgwWenKai](https://github.com/lxgw/LxgwWenKai) |

本地编译时，系统字体（Songti SC / Heiti SC / Kaiti SC 等）会优先使用；缺失时自动回落到 `fonts/` 内的开源字体。

## 项目结构

```
.
├── main.typ          # 主文件（论文入口）
├── whu-thesis.typ    # 模板核心文件
├── logo/             # 校徽等图片资源
├── fonts/            # 打包的中文字体（Noto CJK + LXGW WenKai）
└── demo.pdf          # 示例输出
```

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
