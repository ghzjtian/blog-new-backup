---
title: Jenkins 的安装与使用
tags: [CI]
categories: [CI]
date: 2020-06-13 17:46:19
---

> 记录 Jenkins 在 Mac 上安装与使用的过程

<!-- more -->

## 1.参考
* 1.[Jenkins](https://www.jenkins.io/)
* 2.[Using Jenkins with Xamarin](https://docs.microsoft.com/en-us/xamarin/tools/ci/jenkins-walkthrough)
* 3.[Save Jenkins configuration](https://stackoverflow.com/questions/54192905/how-to-save-jenkins-configuration)
* 4.[Login Credentials Brute Force](https://issues.jenkins-ci.org/browse/JENKINS-30107)
* 5.[Jenkins Github](https://github.com/jenkinsci/jenkins)

## 2.在 Mac mini 上安装 Jenkins
#### 1.下载安装

> [1.Homebrew Installer](https://www.jenkins.io/download/lts/macos/)
> [2.How to Stop, Restart Jenkins - Common URL options](https://damien.co/general/how-to-start-stop-restart-or-reload-jenkins-mac-osx-8022/)
> [3.Update Jenkins from a war file](https://stackoverflow.com/questions/11062335/update-jenkins-from-a-war-file)

* 1.使用 brew 下载

```
brew install jenkins-lts

// 会提示需下载 jdk 8(Jenkins-lts)
brew cask install homebrew/cask-versions/adoptopenjdk8

```

* 2.开始/结束 等控制命令

```
// 作为服务类型去运行
brew services start jenkins-lts
brew services stop jenkins-lts
brew services restart jenkins-lts
```

```
// 作为 命令行 程序去运行
$ jenkins-lts

开启后，可以使用浏览器去控制 Jenkins
// http://[jenkins-server]/[command] where [command] can be
exit -> shutdown jenkins
restart restart jenkins
reload to reload the configuration

如: http://10.100.1.172:8080/restart 去重启 Jenkins
```


##### 2.Jenkins 配置文件

```
~/.jenkins/config.xml
/usr/local/opt/jenkins-lts/homebrew.mxcl.jenkins-lts.plist

任务文件路径:  ~/.jenkins/jobs/[JOB NAME]
任务配置文件路径:  ~/.jenkins/jobs/[JOB NAME]/config.xml
项目文件路径: ~/.jenkins/workspace
```

##### 3.更新
* 1.在 `Manage Jenkins -> System Information` 中可以看到 `jenkins.war` 的文件的路径 `executable-war`，如这里为: 

```
System Properties
Name  			Value   
awt.toolkit	sun.lwawt.macosx.LWCToolkit
BUILD_TIMESTAMP	2020-07-06_02:30:05_CST
executable-war	/usr/local/Cellar/jenkins-lts/2.204.1/libexec/jenkins.war
```
* 2.在搭建的 `Jenkins Server` 中下载新版 `jenkins.war` 包.
* 3.停止 Jenkins: `brew services stop jenkins-lts`
* 4.用新下载的 `jenkins.war` 替换 `/usr/local/Cellar/jenkins-lts/2.204.1/libexec/jenkins.war`
* 5.重启 Jenkins: `brew services start jenkins-lts`
* 6.Jenkins 的环境变量可以在 `http://localhost:8080/env-vars.html/` 看到, 也可以在项目的 `http://localhost:8080/view/Pipeline/job/idds-build-test2/job/test/pipeline-syntax/globals` 看到 Pipeline 的语法.

## 3.设置 Jenkins 中 Shell 的 PATH

> 如果不设置的话，会导致在 terminal 上能正常运行的脚本在 Jenkins 的 `Execute shell` 上不能正常运行.

##### 1.参考
* 1.[jenkins on Mac, PATH is not set right, no /usr/local/bin](https://stackoverflow.com/questions/15620369/jenkins-on-mac-path-is-not-set-right-no-usr-local-bin)

##### 2.操作

* 1.编辑 Jenkins `/usr/local/Cellar/jenkins-lts/2.204.1/homebrew.mxcl.jenkins-lts.plist` 文件，添加 Mac 的 $PATH 到 Jenkins 中.

```
// 输出 PATH
echo $PATH 
```

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>Label</key>
    <string>homebrew.mxcl.jenkins-lts</string>
    <key>ProgramArguments</key>
    <array>
      <string>/usr/libexec/java_home</string>
      <string>-v</string>
      <string>1.8</string>
      <string>--exec</string>
      <string>java</string>
      <string>-Dmail.smtp.starttls.enable=true</string>
      <string>-jar</string>
      <string>/usr/local/opt/jenkins-lts/libexec/jenkins.war</string>
      <string>--httpListenAddress=127.0.0.1</string>
      <string>--httpPort=8080</string>
    </array>
    <key>RunAtLoad</key>
    <true/>
    <key>EnvironmentVariables</key>
    <dict>
        <key>PATH</key>
        <string>(You PATH)</string>
    </dict>
  </dict>
</plist>

```



## 4.源代码管理

> 首次安装完成后会自动安装 Git 插件

## 5.触发机制 

> 一般选择 `Poll SCM`

## 6.Build 的脚本

> 在 Mac 上运行就选择 `Execute shell`, 然后执行的脚本格式跟在 terminal 上一样.


## 7.常用的插件
#### 1.[Build Timestamp](https://stackoverflow.com/a/44011594/5237440)
* 1.让 Jenkins 使用 Timestamp

#### 2.[Email Extension](https://plugins.jenkins.io/email-ext/)
* 1.使 Email 的格式更加丰富

#### 3.[Workspace Cleanup](https://plugins.jenkins.io/ws-cleanup/)
* 1.在每次 Build 前就 Clean 整个项目.

#### 4.[Environment Injector](https://plugins.jenkins.io/envinject/)
* 1.插入 password 等等敏感的数据, 提供 项目 build 变量信息供项目访问.
* 2.但不支持 `Pipeline` 语法.

#### 5.Delivery Pipeline
* 1.可视化 任务管道传递

#### 6.Role-based Authorization
* 1.角色权限管理

#### 7.Pipeline Utility Steps
* 1.Jenkins 常用的 Pipeline 工具.

#### 8.[Pipeline: Basic Steps](https://plugins.jenkins.io/workflow-basic-steps/)
* 1.Jenkins 常用的 Pipeline 命令.

## 8.过程及结果通知

#### 1.参考
* 1.[Jenkins配置邮件提醒](https://www.jianshu.com/p/cb816b42673d)
* 2.[邮件格式定义:Jenkins: Improve the format of the email](https://bytefreaks.net/applications/jenkins-improve-the-format-of-the-email)

#### 2.步骤
* 1.Enable `Configure Global Security` -> `Enable proxy compatibility`
* 2.如设置 QQ ，则需要先 [开启 SMTP 服务](https://service.mail.qq.com/cgi-bin/help?subtype=1&&id=28&&no=331),然后使用返回的授权码代替密码进行登录.
* 3.正确设置 邮件服务器的信息.


#### 3.每个 build 都发送邮件
* 1.[send email at every build](https://shalimatech.com/send-email-every-build-jenkins/)

#### 4.设置格式
* 1.发送人名字设置, 在 `Configure System` -> `System Admin e-mail address` 设置为 `Name<email address>` 格式, 如: `Jenkins server <123@qq.com>`.

#### 5.Eamil 模板参考

```
Hi All,
    <br/>
    <br/>
    $PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS.<br/>
    <br/>
    Click <a href="$BUILD_URL/console">$BUILD_URL/console</a> to view full <strong>console output</strong> results.<br/>
    Click <a href="$JOB_URL/ws/README.md">$JOB_URL/ws/README.md</a> to download the <strong>README.md</strong> file. <br/>
    If you cannot connect to the build server, check the attached logs.<br/>
    <br/>
    --<br/>
    Following is the last 100 lines of the log.<br/>
    <br/>
    --LOG-BEGIN--<br/>
    <pre style='line-height: 22px; display: block; color: #333; font-family: Monaco,Menlo,Consolas,"Courier New",monospace; padding: 10.5px; margin: 0 0 11px; font-size: 13px; word-break: break-all; word-wrap: break-word; white-space: pre-wrap; background-color: #f5f5f5; border: 1px solid #ccc; border: 1px solid rgba(0,0,0,.15); -webkit-border-radius: 4px; -moz-border-radius: 4px; border-radius: 4px;'>
    ${BUILD_LOG, maxLines=100, escapeHtml=true}
    </pre>
    --LOG-END--
    <br/>
    <br/>

From: Mac mini's Jenkins server <$BUILD_TIMESTAMP>
```



## 9.用户管理

> 需要 [`Matrix Authorization Strategy`](https://plugins.jenkins.io/matrix-auth/) 插件

#### 1.参考
* 1.[A way to restrict permissions to a user per individual job in jenkins](https://www.edureka.co/community/47822/there-restrict-permissions-user-per-individual-job-jenkins)
* 2.[Standard Security Setup(wiki.jenkins.io)](https://wiki.jenkins.io/display/jenkins/standard+security+setup)
* 3.[How to Reset Jenkins Admin users Password](http://abhijitkakade.com/2019/06/how-to-reset-jenkins-admin-users-password/)

#### 2.具体操作


* 1.From the jenkins dashboard,click on Manage Jenkins.

* 2.under Manage jenkins->Configure Global Security->select Enable security.

* 3.Under the Authorization section, select the "Project-based Matrix Authorization Strategy"

* 4.Add the particular user and assign the appropriate permissions.(用户必须在这里有 `Overall -> Read` 的权限，否则在子项目配置的权限也会没有效果.)

* 5.And then to assign Job specific permissions :

	* 1.Go to the job (say job1) for which you need to assign permissions.
	
	* 2.Click Configure->under the general tab->Enable Project-based Security.
	
	* 3.Add the particular user (say user1) and assign the required permissions.




## 10.自动打包 `Xamarin.Android` 项目

#### 0.前期准备

##### 1.Mac 安装 xmlstarlet 软件.
* 1.安装 [`xmlstarlet`(Mac xml 解析器)](http://macappstore.org/xmlstarlet/)
	* 1.因为打包后生成的 APK 包需要附上版本号，要读取 `AndroidManifest.xml` 文件才能完成这个操作. 
	* 2.安装: `brew install xmlstarlet`
* 2.使用方法
	* 1.[Extract XML Value in bash script](https://stackoverflow.com/a/17333937/5237440)
	* 2.[XmlStarlet Command Line XML Toolkit User's Guide](http://xmlstar.sourceforge.net/doc/UG/xmlstarlet-ug.html)

* 3.例子

```
// input.xml
<?xml version="1.0" encoding="UTF-8"?>

<Environment xmlns:android="http://schemas.android.com/apk/res/android" xmlns="http://schemas.dmtf.org/ovf/environment/1" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:oe="http://schemas.dmtf.org/ovf/environment/1" xmlns:ve="http://www.vmware.com/schema/ovfenv" oe:id="customerId" ve:vCenterId="centerID" android:versionCode="251" android:versionName="2.4.0" >
  <PropertySection>
<Property oe:key="vami.hostname" oe:value="jal"/>
<Property oe:key="vamitimezone" oe:value="Asia/Kolkata"/>
<Property oe:key="ABC_enable" oe:value="1"/>
<Property oe:key="software_only_installer_name" oe:value="install-r8-0-0-0"/>
<Property oe:key="software_only_staging_dir" oe:value="/media/dir"/>
<Property oe:key="software_only_mount_dir" oe:value="/media/cdrom"/>
  </PropertySection>
</Environment>



$ xmlstarlet sel -t -v "//@android:versionCode" input.xml
// Output: 251

$ xmlstarlet sel -t -v "//@ve:vCenterId" input.xml
// Output: centerID

```

##### 2.把 zipalign 添加到个人目录的环境变量中

> Android 打包需要用到的工具.

###### 1.参考
* 1.[Zipalign - Command not found - MAC terminal](https://stackoverflow.com/a/55135196/5237440)

###### 2.配置 zipalign 环境

```
// 查找 zipalign 位置
$ find ~/Library/Developer/Xamarin -name "zipalign"

// 把 zipalign 放置到 个人环境目录下
$ echo "export PATH=\$PATH:~/Library/Developer/Xamarin/android-sdk-macosx/build-tools/29.0.2" >> ~/.bash_profile && . ~/.bash_profile

// 测试效果
$ zipalign

```

###### 3.实际效果
```
// 模板
zipalign -f -v 4 yourSigned.apk yourFinaleApk

zipalign -f -v 4 $WORKSPACE/BLE_APP.Android/Bin/Release/com.glb.BLE_APP-Signed.apk $WORKSPACE/BLE_APP.Android/Bin/Release/finalApp.apk

```


#### 1.项目参数的保存

* 0.Build Environment

```
Delete workspace before build starts
Add timestamps to the Console Output

Inject passwords to the build as environment variables(STORE_PASS)
```

* 1.Excute shell

```
pwd

whoami

cd MowerGG

nuget restore

```


* 2.Inject Environment

```
KEYSTORE_FILE = /Users/glb_gz/Desktop/GreenworksGreenGuide.keystore
KEYSTORE_ALIAS = GreenworksGreenGuide

APK_BIN_PATH =  $WORKSPACE/MowerGG/MowerGG.Android/bin
MANIFEST_PATH = $WORKSPACE/MowerGG/MowerGG.Android/Properties

```

* 4.Excute shell

```
# 必须放置在这里(这个 Execute shell)，否则后面的执行会读取不到这个值
declare -a Environments=(
                 "Brand1 - Dev2;AndroidManifest1.xml"
                 "Brand2 - Dev2;AndroidManifest2.xml"
                )



StartJarSignAndZip() {

	versionName=$(xmlstarlet sel -t -v "//@android:versionName" "$MANIFEST_PATH"/"$2")
	versionCode=$(xmlstarlet sel -t -v "//@android:versionCode" "$MANIFEST_PATH"/"$2")
	packageName=$(xmlstarlet sel -t -v "//@package" "$MANIFEST_PATH"/"$2")

	INPUT_APK="$APK_BIN_PATH"/"$1"/"$packageName"".apk"
    SIGNED_APK="$APK_BIN_PATH"/"$1"/"$packageName""-Signed.apk"
    FINAL_APK="$APK_BIN_PATH"/"$1"/"$packageName""_$versionName"".$versionCode"".apk"


	jarsigner -verbose -sigalg MD5withRSA -digestalg SHA1 -keystore $KEYSTORE_FILE -storepass $STORE_PASS -signedjar "$SIGNED_APK" "$INPUT_APK" $KEYSTORE_ALIAS

	zipalign -f -v 4 "$SIGNED_APK" "$FINAL_APK"
}



StartMSBuild() {
	msbuild /p:Configuration="$1" /t:PackageForAndroid /t:SignAndroidPackage  MowerGG/MowerGG.Android/Globe.IoT.App.GreenGuide.Android.csproj
	
    StartJarSignAndZip "$1" "$2"
    
}



for environment in "${Environments[@]}"
   do
     echo "$environment"
     configuration=$(echo "$environment" | awk -F';' '{print $1}')
     manifestFileName=$(echo "$environment" | awk -F';' '{print $2}')
     StartMSBuild "$configuration" "$manifestFileName"
   done

```

## 11.打包 `Xamarin.iOS` 项目

#### 1.参考
* 1.[IPA Support in Xamarin.iOS](https://docs.microsoft.com/en-us/xamarin/ios/deploy-test/app-distribution/ipa-support?tabs=macos)

#### 2.过程

```
msbuild /p:Configuration="APP.iOS - Develop" /p:Platform="iPhone" /p:IpaPackageDir="/Users/user/Desktop" /p:BuildIpa=true /t:Build Globe.IoT.App.GreenGuide.iOS.csproj
```






/Users/glb_gz/Documents/Xamarin_Workplace/ggmowerapp/MowerGG/MowerGG.iOS/Globe.IoT.App.GreenGuide.iOS.csproj


## 12.在 `Windows` 上安装

### 1.下载
* 1.下载 [jre8](https://www.oracle.com/java/technologies/javase-jre8-downloads.html)
* 2.下载 [jenkins](https://www.jenkins.io/download/thank-you-downloading-windows-installer-stable/)

### 2.安装
* 1.按提示安装

### 3.配置
* 1.配置 `git.exe` 路径.
* 2.配置 `ssh` private key.

### 4.作为 Node 节点服务器
#### 1.参考
* 1.[Installing Jenkins as a Windows service](https://wiki.jenkins.io/display/JENKINS/Installing+Jenkins+as+a+Windows+service)
* 2.[Jenkins Master and Slave Architecture – A Complete Guide](https://www.edureka.co/blog/jenkins-master-and-slave-architecture-a-complete-guide/)
* 3.[Jenkins Master Slave Configuration](https://www.studytonight.com/jenkins/jenkins-master-slave-configuration)
* 4.[Youtube-Jenkins Master/Slaver](https://www.youtube.com/watch?v=rr-R955N4nM)


#### 2.安装

##### 1.在 Master 机器的 Jenjins 上添加 Node, 然后如下图的配置

* 1.以后每次修改后都需要重新连接 Slave
* 2.添加 Slave 的 Git 执行路径到 配置 `Tool Locations` 中. 
* 3.`Remote root directory` 填写 Slave 保存的项目源码路径.

![](http://pic.pgyjz.cn/blog/Angular/Xnip2021-01-14_12-11-18.png)


##### 2.在 Slave 机器上用浏览器登录 Master 的 Jenkins, 下载 `agent.jar`文件

##### 3.编写 bat 脚本,内容如下，然后保存为 `Jenkins.bat`

```
java -jar D:\Jenkins\agent.jar -jnlpUrl http://10.100.1.172:8081/computer/GZ-Developer-Computer(Slave1)/slave-agent.jnlp -secret 05ddb1dcdfd108fe30f40e194d13c4755af31e65f969b84ed959b3780bbf2310 -workDir "D:\Jenkins\Slave"
```

##### 4.设置脚本开机自动运行
* 1.打开运行，然后输入 `shell:common startup`， 就会打开 `系统启动文件夹`
* 2.把脚本 `Jenkins.bat` 放到 `系统启动文件夹` 下
* 3.但发现以后要登录计算机，才会触发脚本自动运行!!!

##### 5.现在在 Master Jenkins 上可以看到 Slave Jenkins 的相关信息.


#### 3.项目配置
* 1.Git 需要新创建一个 `Credentials` , 如果用 ssh 验证，需要 Slave 机器的 `ssh private key`.
* 2.项目的 `General/Restrict where this project can be run` 填写 `Slave` 的 `Label`


### 5.辅助工具
* 1.[Jenkins Pipeline Linter Connector(VS code plugin)](https://marketplace.visualstudio.com/items?itemName=janjoerke.jenkins-pipeline-linter-connector)


## 13.Multi Pipe line

### 1.参考
* 1.[Jenkins shared library: tutorial with examples](https://tomd.xyz/jenkins-shared-library/)

### 2.内部库

> 因为 Jenkins 认为项目的 Jenkinsfile 脚本是不安全的，并且一些常用的代码共用的原则，所以需要内部库的支持.

#### 1.Jenkins 内部的 workflowLibs 库
* 1.Git remote 为: `origin	ssh://tian@localhost:22222/workflowLibs.git (fetch)`.

#### 2.Git 库
* 1.可以放在 Gitlab 或 Github
* 2.在 `Global Pipeline Libraries ` 配置
	* 1.Name to `pipeline-library`
	* 2.Default version to `master`
	* 3.Select `Modern SCM`/`Git` and input your `Project Repository` and select `Credentials`
	* 4.Save, and each project import this library , this library will auto download to workspace.

### 3.项目 Jenkinsfile 文件的配置及使用

#### 1.Import the library
* 1.Example: `@Library('jenkins-build-script')_`

#### 2.Usage
* 1.Use `executeCommand xxx` or `getDotnetProjectVersion(xxx)` to execute the command in vars.
* 2.Or use `import com.globe.IotXmlParser` to import the class and then execute its command.


#### 3.`Jenkinsfile` Example

```


```

### 4.Master -> Slave 架构上使用 Pipeline
#### 1.有 `shared library` 时
* 1.`library` 会下载到 Master
* 2.`Project code` 会下载到 Slave
* 3.如果需要 `shared library` 读取文件, 不能通过传递文件名让 `shared library` 读取，这样会找不到, 应该用 插件 `Pipeline: Basic Steps ` 的 `readFile` 方法去读取文件内容，再传递到 `shared library` 去处理,但是要注意处理前先去除文件的 `字节顺序标记（英语：byte-order mark，BOM）` 否则会可能出错, 如 Groovy 的 `XmlParser().parseText` 会出现 `org.xml.sax.SAXParseException; lineNumber: 1; columnNumber: 1; Content is not allowed in prolog.` 错误.
* 4.用 `Xcode` 打开文件查看 HEX 的方法: [What's a good hex editor/viewer for the Mac?](https://stackoverflow.com/a/10237422/5237440)







