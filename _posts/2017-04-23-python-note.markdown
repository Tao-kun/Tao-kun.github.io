---
layout: post
title:  "Python 笔记"
date:   2017-04-23 22:36:00 +0800
tags: [Python, Note]
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
>>> os.remove("filename")
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

## json 模块
```
>>> json.dump(object. filename)    # 打包 Python 对象为 JSON 文件
>>> json.dumps(object)    # 打包 Python 对象为 JSON 数据(str)
>>> json.load(filename)    # 从 JSON 文件读取为 Python 对象
>>> json.loads(json_str)    # 从 JSON 字符串读取为 Python 对象
```
