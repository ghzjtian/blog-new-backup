---
title: VS Code 
tags: [IDE]
categories: [IDE]
date: 2020-08-11 17:46:19
---



### Visual Studio Code 使用记录

<!-- more -->



# 1.IDE 资料
* 1.[第一次使用VS Code时你应该知道的一切配置](https://juejin.im/post/6844903826063884296)
* 2.[VS Code Doc](https://code.visualstudio.com/docs/languages/html)
* 3.[VS Code settings you should customize](https://dev.to/thegeoffstevens/vs-code-settings-you-should-customize-5e75)
* 4.[MacOS shortcuts](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf)
* 5.[Recommended VS Code Extensions for Angular Developers](https://johnpapa.net/rec-ng-extensions/)
* 6.[7 must-have Visual Studio Code extensions for Angular](https://medium.com/frontend-coach/7-must-have-visual-studio-code-extensions-for-angular-af9c476147fd)
* 7.[22 Best Visual Studio Code Extensions for Web Development](https://scotch.io/bar-talk/22-best-visual-studio-code-extensions-for-web-development)
* 8.[JavaScript (ES6) code snippets](https://marketplace.visualstudio.com/items?itemName=xabikos.JavaScriptSnippets)

## 2.VS Code 插件
* 1.[CSS Peek<在 HTML 页面点击 CSS Class 名字，会跳转到 CSS 文件的 Class 处>](https://marketplace.visualstudio.com/items?itemName=pranaygp.vscode-css-peek)
* 2.`GitLens`<在当前行中查看提交者>
* 3.`open in browser` 右键文件可以选择 `浏览器中预览网页`
* 4.[VS Code .csproj](https://marketplace.visualstudio.com/items?itemName=lucasazzola.vscode-csproj)
* 5.[C#](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)
* 6.[Material Icon Theme](https://marketplace.visualstudio.com/items?itemName=PKief.material-icon-theme)
* 7.[Atom One Light Theme](https://marketplace.visualstudio.com/items?itemName=akamud.vscode-theme-onelight)
* 8.[Debugger for Chrome](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome)
* 9.[vscode-angular-html](https://marketplace.visualstudio.com/items?itemName=ghaschel.vscode-angular-html)
* 10.[Angular 10 Snippets](https://marketplace.visualstudio.com/items?itemName=Mikael.Angular-BeastCode)
* 11.[TSLint](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-typescript-tslint-plugin&wt.mc_id=devto-blog-jopapa)
* 12.[Angular Follow Selector](https://marketplace.visualstudio.com/items?itemName=sanderledegen.angular-follow-selector)
* 13.[JavaScript (ES6) code snippets](https://marketplace.visualstudio.com/items?itemName=xabikos.JavaScriptSnippets)
* 14.[johnpapa.angular2](https://marketplace.visualstudio.com/items?itemName=johnpapa.Angular2)


## 3.用 VS Code 开发 .Net Core 项目

### 1.参考
* 1.[Working with C#](https://code.visualstudio.com/docs/languages/csharp)
* 2.[Using .NET Core in Visual Studio Code](https://code.visualstudio.com/docs/languages/dotnet)
* 3.[Your First ASP.NET Core Application on a Mac Using Visual Studio Code](https://jakeydocs.readthedocs.io/en/latest/tutorials/your-first-mac-aspnet.html)

### 2.步骤
* 1.下载 `.NET Core`
* 2.下载 `C# extension`
* 3.创建项目 `dotnet new console`
* 4.下载 HTTPS 支持: `dotnet dev-certs https --trust`
* 5.到项目目录下，运行 `dotnet run`, 或者项目文件 `launch.json` 配置启动项后按 F5 即可启动.


## 4.快捷键

### 1.参考
* 1.[Jump to Closing tag in VS Code](https://stackoverflow.com/a/49681162/5237440)
* 2.[Code Navigation](https://code.visualstudio.com/docs/editor/editingevolved)
* 3.[Command Palette](https://code.visualstudio.com/docs/getstarted/userinterface#_command-palette)

### 2.快捷键记录
* 1.`⇧⌘M` 显示 错误/问题 面板.
* 2.`F8` 导航到当前编辑页面的错误位置.
* 3.`⇧⌥F` 去格式化整个文档, 或者按 `⌘K` 然后  `⌘F` 去格式化选中的文档.
* 4.`⇧⌘\` 导航到 开始或结束的 `括号{}`
* 5.`⌘P` 快速搜索并打开一个文件.
* 6.`⌘P` will let you navigate to any file or symbol by typing its name
* 7.`⌃Tab` will cycle you through the last set of files opened
* 8.`⇧⌘P` will bring you directly to the editor commands
* 9.`⇧⌘O` will let you navigate to a specific symbol in a file
* 10.`⌃G` will let you navigate to a specific line in a file
* 11.`⌘K Z`全屏模式, 按两次 `Esc` 退出.
* 12.`⌘D` [选择当前光标所在的单词.](https://code.visualstudio.com/docs/editor/codebasics#_multiple-selections-multicursor)
* 13.[`⌥⌘[` 折叠, `⌥⌘]` 不折叠 代码.](https://code.visualstudio.com/docs/editor/codebasics#_folding)
* 14.[`F7` 显示下一个 Git 对比不同点](https://code.visualstudio.com/docs/editor/versioncontrol)
* 15.[`⇧⌘C` 打开外部 Terminal](https://code.visualstudio.com/docs/editor/integrated-terminal)




