---
title: Git 的学习
tags: [Git]
categories: [Git]
date: 2020-04-01 17:46:19
---

> 记录 Git 一些常用的命令.

<!-- more -->



## 0.参考
* 1.[Git scm](https://git-scm.com/)
* 2.[git-stash用法小结](https://www.cnblogs.com/tocy/p/git-stash-reference.html)
* 3.[GUI Clients](https://git-scm.com/download/gui/mac)
* 4.[git clean用法](https://www.cnblogs.com/lsgxeva/p/8540476.html)

## 1.Git stash

#### 1.显示 Git Stash 列表

```
$ git stash list
stash@{0}: On develop: ABC-613
stash@{1}: On develop: Try to improve the network logic.
stash@{2}: On develop: Add agm/core component.

```

#### 2.Git stash save

* 1.保存

```
$ git stash save "ABC-602 front-end company UI"
Saved working directory and index state On develop: A3S-602 front-end company UI

```

* 2.然后列表情况.

```
$ git stash list
stash@{0}: On develop: ABC-602 front-end company UI
stash@{1}: On develop: ABC-613
stash@{2}: On develop: Try to improve the network logic.
stash@{3}: On develop: Add agm/core component.

```

#### 3.应用缓存的 stash 

```
# 不删除 stash
$ git stash apply stash@{1}
# 删除 stash
$ git stash pop

```

#### 4.移除 stash

```
$ git stash list
stash@{0}: On develop: ABC-602 front-end company UI
stash@{1}: On develop: ABC-613
stash@{2}: On develop: Try to improve the network logic.
stash@{3}: On develop: Add agm/core component.

$ git stash drop stash@{1}
Dropped stash@{1} (c68cea2c0f6e246ac6c8021ef512516491960df9)

$ git stash list
stash@{0}: On develop: ABC-602 front-end company UI
stash@{1}: On develop: Try to improve the network logic.
stash@{2}: On develop: Add agm/core component.

```

## 2.Git tag

#### 1.参考
* 1.[Git 基础 - 打标签](https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E6%89%93%E6%A0%87%E7%AD%BE)


#### 2.命令
##### 1.查看 tag list


```
git tag

```


##### 2.打 tag

```
git tag -a test/frontend/v1.5.2.90 -m "Update front-end version to v1.5.2.90"
```

##### 3.上传 tag 到远程库

```
// 推送一个
git push origin v1.5
推送全部
git push origin --tags
```


## 3.从其它分支选择指定的 commit 到当前分支中

* 1.参考:
	* [git cherry-pick 教程](http://www.ruanyifeng.com/blog/2020/04/git-cherry-pick.html)
	* [SCM cherry-pick](https://git-scm.com/docs/git-cherry-pick)

* 2.步骤

```
git cherry-pick <HashA> <HashB>
``` 







git tag -a test/frontend/v1.5.3.93 -m "Update front-end version to v1.5.3.93"




## 4.设置代理

> 国内访问 github 很慢，需要设置代理.
> 如果代理不正确，会有 `fatal: unable to access 'https://github.com/docker/getting-started.git/': LibreSSL SSL_connect: SSL_ERROR_SYSCALL in connection to github.com:443 ` 的错误.

###  1.参考
* 1.[SETTING PROXY FOR GIT ON MAC!](https://shellzero.wordpress.com/2012/05/30/setting-proxy-for-git-on-mac/)
* 2.[SSL_connect: SSL_ERROR_SYSCALL in connection to github.com:443](https://stackoverflow.com/a/49789726/5237440)

### 2.步骤

```
Step1:Open your terminal.

Step2: Type the command  git config –global http.proxy [your proxy website or the ip address]

         For example: git config –global http.proxy http://10.11.32.9:8888

Step3: You can now check what are the settings configured in the gitconfig by executing the following command

Zerocools-MacBook:~ pamusriharsha$  git config –list

For example: It would be something as this

user.name=applecool
                            user.email=applecoolkmit@gmail.com
                            http.proxy=http://10.11.32.9:8888

That’s it here we go. Your proxy settings for your git is successfully completed! 😀
```



