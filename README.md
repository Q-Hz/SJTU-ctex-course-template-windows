# 上海交通大学课程大作业论文模板（Windows 适配版）

[![](https://img.shields.io/badge/sharelatex-deprecated-lightgrey.svg)](https://www.sharelatex.com/templates/5a03fcddc4aab43a4a6226e2)

这是为撰写上海交通大学课程作业、课程设计而准备的 XeLaTeX 模板，非官方出品。**本版本面向 Windows 用户，已修复旧版模板的三处编译问题，并在 Windows + TeX Live 2024 环境中完成 XeLaTeX 编译验证。** 生成的课程论文示例参见 [thesis.pdf](./thesis.pdf)。

本版本基于本目录中的 SJTU-TermPaper 旧版课程论文模板（`sjtuthesis 2017/02/19 v0.9.5`）修改。

当前上游项目为 [sjtug/SJTUThesis](https://github.com/sjtug/SJTUThesis)。本页的修复记录与验证结果仅适用于本目录中的旧版课程论文模板，不表示当前上游版本存在相同问题。若后续 Fork 当前上游仓库，需要根据该仓库的文件结构另行整合、验证。

## Windows 编译

### 环境要求

- Windows，并安装可用的 TeX Live 及模板所需宏包；本机验证使用 TeX Live 2024。
- 使用 XeLaTeX 编译主文件 `thesis.tex`，参考文献后端为 Biber。
- 系统中需有宋体（SimSun）、黑体（SimHei）、楷体（KaiTi）、仿宋（FangSong）。本版本默认使用 `fontset=windows`，无需安装 Adobe 中文字体。
- `xelatex`、`biber` 应可在终端中调用；安装发行版后若找不到命令，请检查 PATH 或重新打开终端。

### 编译步骤

在 `thesis.tex` 所在目录打开 PowerShell 或命令提示符，依次执行：

```text
xelatex -interaction=nonstopmode -halt-on-error -file-line-error thesis.tex
biber thesis
xelatex -interaction=nonstopmode -halt-on-error -file-line-error thesis.tex
xelatex -interaction=nonstopmode -halt-on-error -file-line-error thesis.tex
```

输出文件为 `thesis.pdf`。在图形编辑器中，请将主文件设为 `thesis.tex`，选择 XeLaTeX 编译器及 Biber 参考文献工具，按相同顺序编译。

### 修复记录

| 文件 | 原问题 | 本版本修复 |
| --- | --- | --- |
| `thesis.tex` | 强制使用 `fontset=adobe`；缺少 Adobe 字体时出现 `The font "AdobeSongStd-Light" cannot be found`。 | 改为 `fontset=windows`，使用本机 Windows 中文字体。 |
| `sjtuthesis.cls` | 在声明 `bi-first`、`bi-second` 题注选项之前调用它们，触发 `Package caption Error: bi-first undefined`。 | 先执行 `\DeclareCaptionOption`，再执行对应的 `\captionsetup`。 |
| `sjtuthesis.cfg` | 学位类型判断中缺少一个 `\fi`，导致条件未闭合的诊断信息。 | 补齐 `\fi`，闭合嵌套条件。 |

其中字体设置是本版本针对 Windows 的默认配置；题注选项顺序和条件闭合问题属于旧版模板代码问题。

补充排版修正：页脚总页数改用已加载的 `lastpage` 宏包提供的 `LastPage` 标签，避免增加附录内容后仍显示总结页的页码。

### 验证范围与提示

2026 年 10 月 28 日，在本机 Windows + TeX Live 2024 环境中完成 XeLaTeX → Biber → XeLaTeX → XeLaTeX 编译验证，成功生成 PDF。验证针对本仓库当前启用的示例内容，不代表已覆盖所有 Windows、TeX 发行版或模板功能组合。

当前示例正文没有文献引用，因此可能出现 `Empty bibliography` 或 Biber 的无引用提示；加入实际引用后再按上述顺序编译即可。字体尺寸替代、行宽超出等排版警告不等同于编译失败。

附录中的 Windows 使用说明及修复记录见 [`tex/app_setup.tex`](./tex/app_setup.tex)。此版本默认面向 Windows；在 macOS、Linux 或在线平台上使用时，应另行选择当地可用的 CTeX 字体配置并重新验证。

## 论文效果

<p align="center">
      <a><img src="./cover.png" width="300"></a>
</p>



## 问题诊断

编译失败时，按上面的步骤手动逐次编译，并查看 `thesis.log` 中的首个错误；参考文献处理问题查看 `thesis.blg`。确认正在编译主文件 `thesis.tex`，并且当前工作目录是模板根目录。


## 软件许可证

上海交通大学校徽图片(`sjtulog.png`)和横幅图片(`sjtubanner.png`)的版权归原作者所有。其他部分使用 [Apache License 2.0](LICENSE) 授权。
