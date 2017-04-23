---
layout: post
title:  "Pytohn 笔记"
date:   2017-04-22 12:25:00 +0800
categories: main
---

Python的笔记，不定期更新。


## os模块

### 系统类型
```
>>> os.name   
>>> os.uname()
```

### 执行系统命令
```
>>> os.system("ls")
```

### 工作路径
```
>>> os.getcwd()
```

### 返回目录文件（夹）
```
#相对于os.getcwd
>>> os.listdir()
```

```

>>> os.listdir("/usr")
```

### 删除文件
```
>>> os.remove("filwname")
```

### 删除单级目录
```
>>> os.rmdir("dirname")
```

### 重命名文件
```
>>> os.rename("oldname", "newname")
```

### 创建文件夹
```
>>> os.makedirs("/usr/lib/newdir")
```

### 路径分隔符
```
>>> os.sep
```

### 行终止符
```
>>> os.linesep
```

### 当前绝对路径
```
>>> os.path.abspath("path")
```

### 判断文件/目录
```
>>> os.path.isfile("/bin/ls")
>>> os.path.isdir("/bin")
```

### 文件/目录信息
```
>>> os.stat("/bin")
```

### 路径构造
```
>>> os.path.join("c:\\", "Windows", "Fonts")
```

```
>>> os.path.join("/usr", "bin")
```