# 个人简历

本项目为个人简历 Latex 源码存放，同时包含效果图呈现，简历入口为 resume-zh_CN.tex， 修改自项目 [resume](https://github.com/billryan/resume/)，若不想本地手动编译可以将该源码打包至 zip 直接上传至 ShareLatex 进行在线编译与预览。

## 项目说明

一个优雅的 \LaTeX\ 简历模板, 使用 \XeLaTeX\ 编译, 因为受不了古老的`res`和不太适合作为一页纸简历的`moderncv`, 遂自己动手写了这个模板， 受以下项目启发：

- [zachscrivena/simple-resume-cv](https://github.com/zachscrivena/simple-resume-cv)
- [res](https://www.ctan.org/pkg/res)
- [JianXu's CV](http://www.jianxu.net/en/files/JianXu_CV.pdf)
- [paciorek's CV/Resume template](http://www.stat.berkeley.edu/~paciorek/computingTips/Latex_template_creating_CV_.html)
- [How to write a LaTeX class file and design your own CV (Part 1) - ShareLaTeX](https://www.sharelatex.com/blog/2011/03/27/how-to-write-a-latex-class-file-and-design-your-own-cv.html)

*注：由于使用到 `fontspec` 包，编译器需选择 XeLaTeX。*

## 特性

- 极其容易定制和扩展 (`res`模板中枪倒地...)
- 完善的 Unicode 字体支持, 因为用的是 \XeLaTeX\ 嘛
- 完美的中文支持，使用 Adobefonts
- 支持 FontAwesome 4.3.0 (目前还不支持使用别名)

### 效果输出

![resume-zh_CN.png](./resume.preview.png)

## 使用方法

1. OverLeaf 在线编译
2. 使用较新的 \LaTeX\ 发行版在本地计算机编译

### macOS / VS Code 本地预览

安装 MacTeX 或 BasicTeX，以及 VS Code 的 LaTeX Workshop 扩展。本项目的
[工作区配置](.vscode/settings.json) 使用 `/Library/TeX/texbin/xelatex` 编译两次，
不依赖从 Dock 启动的 VS Code 是否继承了终端的 PATH；同时禁用扩展的 magic
comment 编译入口，避免文件首行的 `xelatex` 覆盖工作区中的绝对路径配置。
其他系统需将配置中的 `xelatex` 和 `kpsewhich` 路径改为本机安装位置。

BasicTeX 是精简发行版，需要补齐模板依赖。已有 `xeCJK`、`xltxtra` 等依赖时，
可在用户目录安装缺失的包，无需管理员权限：

```bash
# 仅在尚未初始化用户 TeX 树时执行
/Library/TeX/texbin/tlmgr init-usertree
/Library/TeX/texbin/tlmgr --usermode install realscripts xifthen ifmtarg enumitem nth
```

打开 `resume-zh_CN.tex`，运行 `LaTeX Workshop: Build LaTeX project`，
然后运行 `LaTeX Workshop: View LaTeX PDF file`。PDF 和辅助文件输出到
`build/`，不会覆盖项目中的图片或 PDF 素材。Overleaf 中仍选择 XeLaTeX，
无需使用本地 VS Code 配置。

如果确定只需要中文简历的话单独克隆 `master` 分支即可, 需要注意的是该分支包含 Adobe 的宋楷黑仿四套中文字体，压缩包约为37MB。[下载地址](https://github.com/hijiangtao/resume/releases)

```
git clone https://github.com/hijiangtao/resume.git --branch master --depth 1 --single-branch <folder>
```

如果系统已确定安装有 Adobe 的四套中文字型，在文档的开始处使用包`zh_CN-Adobefonts_internal`, 如果没有安装则使用包`zh_CN-Adobefonts_external`, 在 ShareLaTeX 上编译需要使用包`zh_CN-Adobefonts_external`.

其他具体使用可参考给出的范例，都是极其简单易懂的宏，建议先看看 [How to write a LaTeX class file and design your own CV (Part 1) - ShareLaTeX](https://www.sharelatex.com/blog/2011/03/27/how-to-write-a-latex-class-file-and-design-your-own-cv.html) 和 [How to write a LaTeX class file and design your own CV (Part 2) - ShareLaTeX](https://www.sharelatex.com/blog/2013/06/28/how-to-write-a-latex-class-file-and-design-your-own-cv.html) 了解下该模板的简单背景，下面就一些新定义的宏做简要介绍。

### 宏

- `\name`: 姓名
- `\contactInfo`: 联系信息, 需要三项信息，分别是{邮箱}{手机号}{个人主页}
- `\basicContactInfo`: 简要的联系信息, 需要 项信息, 分别是{邮箱}{手机号}, 没有个人主页的用这个
- `\section`: 用于分节, 如教育背景, 实习/项目经历等
- `\subsection`: 用于小节标题, 无日期选项
- `\datedsubsection`: 用于小节标题, 简历中使用最广，第二项为时间区间，自动右对齐
- `\itemize`: 清单列表，简历中应用最广
- `\enumerate`: 枚举列表，数字标号

### FontAwesome

首先在 [Font Awesome Icons](http://fortawesome.github.io/Font-Awesome/icons/) 上选中自己想使用的图标(暂不支持 alias)，然后在 [fontawesome.sty](https://github.com/billryan/resume/blob/zh_CN/fontawesome.sty) 中找到相应的宏, 将其作为普通文本一样使用。

其他的可以自行参考相应 cls 和 tex 文件。

## License

[The MIT License (MIT)](http://opensource.org/licenses/MIT)

Copyrighted fonts are not subjected to this License.
