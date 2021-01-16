---
title: Cmd 命令学习
tags: [windows]
categories: [windows]
date: 2021-01-16 17:46:19
---



# Cmd 命令学习

> 学习 Windows Cmd.exe 的命令

<!-- more -->

## 1.参考
* 1.[How to create and run batch file on Windows 10](https://www.windowscentral.com/how-create-and-run-batch-file-windows-10)
* 2.[Populating Array in DOS Batch Script](https://superuser.com/questions/191224/populating-array-in-dos-batch-script)
* 3.[Create list or arrays in Windows Batch](https://stackoverflow.com/questions/17605767/create-list-or-arrays-in-windows-batch)

## 2.生成脚本
#### 1.打开记事本
#### 2.输入以下脚本

```
@ECHO OFF
ECHO Congratulations! Your first batch file executed successfully.
PAUSE
```

#### 3.输出到文件

* 1.在 ECHO 命令行的后面添加 >>(add) 或 >(new), 如上面脚本输出到文件 OUTPUT.txt

```
@ECHO OFF
ECHO Congratulations! Your first batch file executed successfully. >> OUTPUT.txt
PAUSE
```

#### 3.另存为 `first_basic_batch.bat` 文件

#### 4.双击运行脚本(或用管理员身份进入脚本目录，然后输入脚本名字，按 Enter ), 会有以下输出

```
Congratulations! Your first batch file executed successfully.
请按任意键继续. . .
```


## 3.命令
### 1.示例

#### 1.输出 string array

```
@echo off 
::set list=C:\Windows\System32\cmd.exe C:\Windows\System32\cmd.exe2 C:\Windows\System32\cmd.exe3 

set list=C:\Windows\System32\cmd.exe
set list=%list%;C:\Windows\System32\cmd.exe2
::set list=%list%;C:\Windows\System32\cmd.exe3
set list=%list%;C:\Windows\System32\cmd.exe4
set list=%list%;C:\Windows\System32\cmd.exe5

(for %%a in (%list%) do ( 
   echo ############ Worker Start
   echo %%a 
   echo ############ Worker End
   echo\
))

PAUSE
```

结果:

```
############ Worker Start
C:\Windows\System32\cmd.exe
############ Worker End

############ Worker Start
C:\Windows\System32\cmd.exe2
############ Worker End

############ Worker Start
C:\Windows\System32\cmd.exe4
############ Worker End

############ Worker Start
C:\Windows\System32\cmd.exe5
############ Worker End

请按任意键继续. . .
```


## 4.计划任务

### 1.循环任务
* 1.打开 `Task Schedule` 程序.
* 2.创建一个每天定时任务.

### 2.开机启动
* 1.打开运行
* 2.输入 `shell:startup`
* 3.复制脚本到弹出的 `C:\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup` 目录下


