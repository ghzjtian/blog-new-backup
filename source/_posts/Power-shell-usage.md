---
title: Powershell 的用法
tags: [Mac]
categories: [Mac]
date: 2019-12-29 17:46:19
---


> 记录 Mac 上 Powershell 的安装及使用

<!-- more -->

## 1.参考
## 2.Mac 安装 Powershell
## 3.Powershell 使用


***
***
***

## 1.参考

* 1.[Installing PowerShell Core on macOS](https://docs.microsoft.com/en-us/powershell/scripting/install/installing-powershell-core-on-macos?view=powershell-6)
* 2.[Multiple foreground colors in PowerShell in one command](https://stackoverflow.com/questions/2688547/multiple-foreground-colors-in-powershell-in-one-command)
* 3.[Run PowerShell 脚本](https://yanxyz.github.io/powershell/scripts/)
* 4.[Learn PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/learn/ps101/00-introduction?view=powershell-7.1)

## 2.Mac 安装 Powershell

```
//  install PowerShell from brew.
brew cask install powershell

```

```
// 进入 Powershell
$: pwsh

PowerShell 7.1.0
Copyright (c) Microsoft Corporation.

https://aka.ms/powershell
Type 'help' to get help.

PS /Users/glb_gz>

```

```
// 退出 Powershell
exit
```

## 3.Powershell 使用

### 1.常用命令
* 1.输出

```
Write-Host "Blue" -ForegroundColor Blue
```

* 2.退出

```
exit 0
```

* 3.方法

```
// 无参
function listAllExchange {
}
listAllExchange

// 一个参数
function customEchoRed($message) {
    Write-Host $message -ForegroundColor Red
}
customEchoRed("abc")

// 多个参数
function executeCommand($message, $rabbit_mq_command){
}
executeCommand "List all exchanges"  "rabbitmqadmin list exchanges"
```


### 2.IDE
#### 1.VS code
* 1.安装插件 [PowerShell](https://marketplace.visualstudio.com/items?itemName=ms-vscode.PowerShell)

### 3.运行 PowerShell 文件
* 1.Mac 在 Terminal 运行 `pwsh` 命令.

```
$ pwsh
```

* 2.如要执行的文件为 `test.ps1`, 则输入 `./test.ps1` 即可.
