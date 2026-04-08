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
typst compile main.typ
```

## 项目结构

```
.
├── main.typ          # 主文件（论文入口）
├── whu-thesis.typ    # 模板核心文件
├── logo/             # 校徽等图片资源
├── pages/            # 附加页面
├── ref/              # 参考文献
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
