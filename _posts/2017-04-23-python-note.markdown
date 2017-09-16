---
layout: post
title:  "Python 笔记"
date:   2017-04-23 22:36:00 +0800
tags: [Python, Note]
---

Python的笔记，不定期更新.

## os模块

### 系统类型
```python
>>> os.name
```

### 执行系统命令
```python
>>> os.system("ls")
```

### 工作路径
```python
>>> os.getcwd()
```
### 更改工作路径
```python
>>> os.chdir(path)
```
### 返回目录文件（夹）
```python
#相对于os.getcwd
>>> os.listdir()
```

```python
>>> os.listdir("/usr")
```

### 删除文件
```python
>>> os.remove("filename")
```

### 删除单级目录
```python
>>> os.rmdir("dirname")
```

### 重命名文件
```python
>>> os.rename("oldname", "newname")
```

### 创建文件夹
```python
>>> os.makedirs("/usr/lib/newdir")
```

### 路径分隔符
```python
>>> os.sep
```

### 行终止符
```python
>>> os.linesep
```

### 当前绝对路径
```python
>>> os.path.abspath("path")
```

### 判断文件/目录
```python
>>> os.path.isfile("/bin/ls")
>>> os.path.isdir("/bin")
```

### 文件/目录信息
```python
>>> os.stat("/bin")
```

### 路径构造
```python
>>> os.path.join("c:\\", "Windows", "Fonts")
```

```python
>>> os.path.join("/usr", "bin")
```

## json 模块
```python
# 序列化
>>> json.dump(object. filename)    # 打包 Python 对象为 JSON 文件
>>> json.dumps(object)    # 打包 Python 对象为 JSON 字符串
# 反序列化
>>> json.load(filename)    # 从 JSON 文件读取为 Python 对象
>>> json.loads(json_str)    # 从 JSON 字符串读取为 Python 对象
```
