---
title: 【小白】brew命令使用
tags:
  - MacOS
  - Brew
categories:
  - Brew
toc: true
abbrlink: 38833
date: 2021-07-25 13:22:08
---

# 一：官网

[HomeBrew](https://brew.sh/)

<!--more-->

# 二：目录

- 安装

- 查看帮助信息

- 查看版本

- 更新HomeBrew自己

- 安装软件包

- 查询可更新的包

- 更新包（formula）

- 清理旧版本

- 锁定不想要的包

- 卸载安装包

- 查看包信息

- 查看安装列表

- 查询可用包

- 卸载HomeBrew

  

# 三：常用命令

- 安装

  ```
  //安装依赖工具
  xcode-select --install
  
  /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
  ```

- 查看帮助信息

  ```
  brew help
  ```

- 查看版本

  ```
  brew -v
  ```

- 更新HomeBrew自己

  ```
  brew update
  ```

- 安装软件包

  ```
  brew install [包名]
  
  //安装git
  brew install git
  
  //安装git-lfs
  brew install git-lfs
  
  //安装wget
  brew install wget
  
  //安装openssl
  brew install openssl
  ```

- 查询可更新的包

  ```
  brew outdated
  ```

- 更新包（formula）

  ```
  //更新所有
  brew upgrade
  
  //更新指定包
  brew upgrade [包名]
  ```

- 清理旧版本

  ```
  //清理所有包的旧版本
  brew cleanup 
  
  //清理指定包的旧版本
  brew cleanup [包名]
  
  //查看可清理的旧版本包，不执行实际操作
  brew cleanup -n 
  ```

- 锁定不想要的包

  ```
  //锁定某个包brew pin $FORMULA  //取消锁定brew unpin $FORMULA     
  ```

- 卸载安装包

  ```
  brew uninstall [包名]//例：卸载gitbrew uninstall git
  ```

- 查看包信息

  ```
  brew info [包名]
  ```

- 查看安装列表

  ```
  brew list
  ```

- 查询可用包

  ```
  brew search [包名]
  ```

- 卸载HomeBrew

  ```
  cd `brew --prefix`rm -rf Cellarbrew prunerm `git ls-files`rm -r Library/Homebrew Library/Aliases Library/Formula Library/Contributionsrm -rf .gitrm -rf ~/Library/Caches/Homebrew
  ```

  

