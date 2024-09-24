---
title: pip 换源
date: 2020-9-23
categories: []
---

解决pip安装时各种readtimeout问题

即刻芜湖起飞

<!-- more  -->

新建py文件(文件名随意)，复制以下代码

```python
import os
 
ini="""[global]
index-url = https://pypi.doubanio.com/simple/
[install]
trusted-host=pypi.doubanio.com
"""
pippath=os.environ["USERPROFILE"]+"\\pip\\"
 
if not os.path.exists(pippath):
    os.mkdir(pippath)
 
with open(pippath+"pip.ini","w+") as f:
    f.write(ini)
```

之后在命令行运行，即可成功。