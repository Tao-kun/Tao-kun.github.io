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
>>> json.dump(object, fp)    # 打包 Python 对象为 JSON 文件
>>> json.dumps(object)    # 打包 Python 对象为 JSON 字符串
# 反序列化
>>> json.load(fp)    # 从 JSON 文件读取为 Python 对象
>>> json.loads(json_str)    # 从 JSON 字符串读取为 Python 对象
```


## Numpy/Scipy/Matplotlib

### 实时动图

```python
import numpy as np
import matplotlib.pyplot as plt

plt.axis([0, 100, 0, 1])
plt.ion()

for i in range(100):
    y = np.random.random()
    plt.scatter(i, y)
    plt.pause(0.1)
```

```python
import numpy as np
from matplotlib import pyplot as plt
from matplotlib import animation

# first set up the figure, the axis, and the plot element we want to animate
fig = plt.figure()
ax1 = fig.add_subplot(2,1,1,xlim=(0, 2), ylim=(-4, 4))
ax2 = fig.add_subplot(2,1,2,xlim=(0, 2), ylim=(-4, 4))
line, = ax1.plot([], [], lw=2)
line2, = ax2.plot([], [], lw=2)

def init():    
    line.set_data([], [])
    line2.set_data([], [])
    return line,line2

# animation function.  this is called sequentially
def animate(i):  
    x = np.linspace(0, 2, 100)     
    y = np.sin(2 * np.pi * (x - 0.01 * i))
    line.set_data(x, y)        
    x2 = np.linspace(0, 2, 100)
    y2 = np.cos(2 * np.pi * (x2 - 0.01 * i))* np.sin(2 * np.pi * (x - 0.01 * i))
    line2.set_data(x2, y2)
    return line,line2

anim1=animation.FuncAnimation(fig, animate, init_func=init,  frames=50, interval=10)
plt.show()
```

```python
import numpy as np
import matplotlib.pyplot as plt
from matplotlib import animation

# New figure with white background
fig = plt.figure(figsize=(6,6), facecolor='white')

# New axis over the whole figure, no frame and a 1:1 aspect ratio
ax = fig.add_axes([0, 0, 1, 1], frameon=False, aspect=1)

# Number of ring
n = 50
size_min = 50
size_max = 50 ** 2

# Ring position
pos = np.random.uniform(0, 1, (n,2))

# Ring colors
color = np.ones((n,4)) * (0,0,0,1)
# Alpha color channel geos from 0(transparent) to 1(opaque)
color[:,3] = np.linspace(0, 1, n)

# Ring sizes
size = np.linspace(size_min, size_max, n)

# Scatter plot
scat = ax.scatter(pos[:,0], pos[:,1], s=size, lw=0.5, edgecolors=color, facecolors='None')

# Ensure limits are [0,1] and remove ticks
ax.set_xlim(0, 1), ax.set_xticks([])
ax.set_ylim(0, 1), ax.set_yticks([])

def update(frame):
    global pos, color, size

    # Every ring is made more transparnt
    color[:, 3] = np.maximum(0, color[:,3]-1.0/n)

    # Each ring is made larger
    size += (size_max - size_min) / n

    # Reset specific ring
    i = frame % 50
    pos[i] = np.random.uniform(0, 1, 2)
    size[i] = size_min
    color[i, 3] = 1

    # Update scatter object
    scat.set_edgecolors(color)
    scat.set_sizes(size)
    scat.set_offsets(pos)
    
    # Return the modified object
    return scat,

anim = animation.FuncAnimation(fig, update, interval=10, blit=True, frames=200)
plt.show()
```