---
layout: post
title: "Unix类系统的一些命令行Tips"
categories: commandline, tips
---

#### Tips for bash shell

> 获取当前脚本的目录

``` bash
# 可处理目录中有空格的情况
DIR="$( cd "$( dirname "${BASH_SOURCE[0]}")" && pwd )"
# 或者
DIR=$( dirname "$0" )
```

> 复制目录下所有包含特定文本的文件

``` bash
# 将这些文件拷贝一份
$ grep -iR 'pattern' . | cut -d: -f1 | cut -d'/' -f2- | xargs -I{} rsync -avR {} copypath
```

> 替换目录中的特定文本

``` bash
# 比如将当前目录中所有的iPhone 替换为iPhone 4S
$ find . -type f -print0 | xargs -0 perl -pi -e 's/iPhone/iPhone 4S/g'
```

> 批量重命名

``` bash
$ tree
.
├── a
│   ├── a.txt
│   ├── b.txt
│   └── c
│       ├── a.txt
│       ├── b.txt
├── a.txt
├── b.txt
├── c.tar
└── d.tar.gz
# 将当前文件下的每一个.txt文件，改名为_backup.txt
$ for name in `find . -type f -name "*.txt"`
> do
> mv $name `dirname $name`/`basename $name .txt`_backup.txt
> done
$ tree
.
├── a
│   ├── a_backup.txt
│   ├── b_backup.txt
│   └── c
│       ├── a_backup.txt
│       └── b_backup.txt
├── a_backup.txt
├── b_backup.txt
├── c.tar
└── d.tar.gz
```

#### Tips for python 3.x

> 查看汉字的unicode和utf8编码

```python
>>> '严'.encode("unicode-escape")
b'\\u4e25'
>>> '严'.encode("utf8")
b'\xe4\xb8\xa5'
```
