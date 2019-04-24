# Linux

- Linux 系统组成
    - Linux 内核
    - Linux Shell
    - Linux 应用程序
    - Linux 文件系统
- Linux 内核版本识别
    - r.X.y
    - r: 目前发布的 Kernel 版本 > 主版本号
    - X: 偶数-稳定版本，技术-开发中的版本 > 次版本号
    - y: 错误修补的次数 > 修订版本号
- Shell 命令
    - 内部命令（内置命令）ls、cp 等
    - 外部命令（外置命令）gcc、cowsay 等
- Shell 变量
    - 内部变量 **用户不能修改**，系统提供
    - 用户变量 用户建立的
    - 环境变量
- 通配符与转义符
    - \* 匹配任意多个字符->
        - 能匹配文件或者目录名中的“.”
        - 不能匹配首字符是“.”的文件或者目录名
    - ? 匹配任意单个字符
    - \[\-\] 匹配[]内任意一个字符
    - \\ 转义字符
- 标准输入/输出设备
    - STDIN 文件描述符：0 标准输入，键盘
    - STDOUT 文件描述符：1 标准输出，显示器
    - STDERR 文件描述符：2 标准错误，显示器
- 重定向
    - 重定向就是不用标准输入/输出/错误端口，而进行重新指定。
    - 通常重定向到一个文件
    - 使用重定向符
- 重定向符
    - < 输入重定向
    - \> 覆盖式的输出重定向
    - \>\> 追加式的输出重定向
    - 2> 覆盖式的错误输出重定向
    - 2>> 追加式的错误输出重定向 
    - &> 同时实现输出重定向和错误重定向（覆盖式）
- 输出重定向与空设备
    - 空设备（/dev/null）
    - 利用输出重定向到空设备来屏蔽命令输出或错误输出
- 输出重定向举例
    - 输出重定向使用举例
        - `$ ls -l >myfile`
    - 空设备使用举例
        - `$ mycx &> /dev/null`
        - `$ mycx >/dev/null 2>&1`
- 管道
    - 管道是一种先进先出的单向通道（临时文件）
    - 用于将一个命令的标准输出连接到另一个命令的标准输入
    - |
    - `ls -l | grep "^d"`
    - `cat /etc/passwd | grep username`
- Linux 目录结构
    - /
        - boot
        - lib
        - dev
            - fd0
            - hda1
        - usr
        - tmp
        - var
        - home
            - user1
            - user2
                - hello.c
                - folder
        - root
        - sbin
        - bin
        - etc
        - mnt
            - usb
            - cdrom
        - lost-found
- Linux 的目录结构
    - Linux 文件系统采用树形结构文件目录
    - 起点为根目录 /
    - 主要的标准目录
        - /root
        - /home
        - /etc
        - /dev
        - /mnt
    - 特殊目录
        - .
        - ..
        - ~
- 常见的系统配置文件
    - /etc/fstab 文件系统管理配置文件
    - /etc/passwd 用户管理配置文件
    - /etc/shadow 用户口令管理配置文件
    - /etc/group 组账号管理配置文件
    - /etc/gshadow 组口令管理配置文件
- vi 编辑器使用
- 存储系统的挂载（安装）
    - Linux所有文件系统必须挂载在根目录/下的某个子目录中
    - `# mount -t vfat /dev/hda1 /mnt/c`
    - 常见文件系统类型
        - vat - FAT32
        - ntfs - NTFS
        - ext4 - Linux文件系统
        - HPFS - OS/2文件系统
        - UFS - UNIX文件系统
        - iso9600 - CD-ROM文件系统
- 磁盘分区的设备名
    - **/dev/sda5**
    - /dev/ 硬盘设备文件所在目录
    - sd hd表示IDE设备，sd表示SCSI\SAS\SATA设备
    - a 硬盘的顺序号，a、b、c
    - 5 分区的顺序号，1、2、3
- mount
    - `# mount [选项] <挂载设备名称> <挂载点>`
    - 选项
        - -t 挂载的文件系统
        - -o [参数=值]
- unmount
    - `# unmount <设备名称/挂载点>`
- 挂载设备的过程
    - 查看设备 `fdisk -l`
    - 挂载设备 `makdir mount`
    - 访问设备
    - 卸载设备 `unmount`
- 常用 shell 命令
    - cat、tac
        - `cat [options] <filename1>...`
        - `$ cat -v exam2.txt`
        - `$ cat file1 file2 > file3`
    - more/less
        - `more [options] <filename1>...`
        - `$ more -c -10 file`
            - 显示file的内容，每10行显示一次，显示之前先清屏
        - `less [options] <filename1>...`
    - cp
        - `cp [options] <source> <dest>`
            - -R, -r 递归地复制目录及目录内的所有项目
            - -f 强制复制，不管目标是否存在
            - -i 交互式复制，覆盖文件前需要确认
        - `$ cp -i exam1.c /usr/s01/y1.c`
        - `$ cp exam1.c /usr/s01/`
        - `$ cp -r /usr/s01 /usr/s02/`
    - rm
        - `rm [options] <filename>`
            - -r 强制删除
            - -i 删除前提示
            - -r 递归删除
        - `$ rm -i test example`
    - mv
        - `mv [options] <filename>...`
        - `$ mv file file.bak`
    - ln
        - `ln [options] <source> <dest>`
            - -s 创建符号链接，而非硬链接
            - -f 强行创建链接，不论其是否存在
            - -i 覆盖原有文件之前先询问用户
        - `$ ln -s somefile softlinkfile`
        - `$ ln -s somedir softlinkfile`
        - 硬链接特点：
            - 不可跨越文件系统
            - 只有超级用户才可以建立 目录 硬链接
            - 不占用空间（占用极少空间）
        - 软链接特点：
            - 可跨越文件系统，甚至跨越网络（NFS）
            - 如果链接指向的文件从一个目录移动到另一个目录，就无法通过符号链接访问它
            - 占有少量空间，存inode的信息
    - find
        - `find [path] [expression]`
        - 功能：在目录结构中搜索文件，并执行指定的操作。
        - 支持布尔运算符，用-a、-o、! 表示
        - `$ find . -name "main*"`
        - `$find . -name "tmp" -o -name "main*"`
        - `$find . -name "a.out" -o -name "*.o" -a time +7`
    - grep
        - `grep [options] <string> <file>...`
        - 功能：检索文本文件的内容，找到文件中满足匹配模式的文本行显示出来
        - `$grep smith phonebook`
        - `$grep '^s' mybook`
        - `$ls -l | grep ^d` 显示匹配行首第一个字母为d的项
        - `$ls -l | grep ^[^d]` 查看所有行首不为d字母的项
        - `$ls -l | grep \*$` 显示所有以*号结尾的文件
    - touch
        - `touch [options] <file1> [file2 ...]`
        - 功能：生成新的空文件或修改指定文件的访问时间和修改时间记录。
        - `$touch newfile`
        - `$touch file`
        - `$touch -t 201701311200 file`
    - mkdir
        - 创建目录
        - `mkdir [-p] <dirName>...`
        - `$mkdir /home/zyj/folder` 创建一个空目录
        - `$mkdir -p mydoc/FAQ` 创建一个空目录树
        - `$mkdir -p /srv/www/{abc,bcd}/htdocs` 创建/srv/www/abc/htdocs和/srv/www/bcd/htdocs目录
    - rmdir
        - 删除**空目录**
        - `rmdir [-p] <dirName>`
        - `$ rmdir -p /usr/xu/txt`
    - pwd
        - 显示当前工作目录
        - `pwd`
    - cd
        - 切换目录
        - `cd <dirName>`
    - ls
        - 显示文件和目录列表
        - `ls [options] [<name> ...]`
            - -a 列出目录下所有文件，包括以.开头的文件
            - -l 列出文件的详细信息，通常称为“长格式”
            - -R 递归地列出所有子目录下的文件
        - ls命令的-l选项显示详细信息，包括访问权限、连接数、所有者、组、文件大小（以字节记）和修改时间
        - ` -rwxr--r-- 1 sarvar faculty163 Apr 11 14:34 mid2 `
        - 第一个字段的第一个字母：
            - 文件类型：
                - - 普通文件
                - b 块特殊文件
                - c 字符特殊文件
                - d 目录
                - l 连接
                - p 命名管道（FIFO）
        - 第一个字段的其他字母：
            - 所有者、组和其他用户的访问权限
            - rwxrwxrwx 前三个是所有者权限，中间三个是同组用户权限，后三个是其他用户权限
            - 每个用户都拥有自己的专属目录（用户主目录），通常放置在/home目录下，这些专属目录的默认权限通常为`drwx------`
        - 第二个字段：
            - 连接数
        - 第三个字段
            - 所有者的登录名
        - 第四个字段
            - 所有者的组名
        - 第五个字段
            - 文件大小，以字节为单位
        - 第六、七、八字段
            - 最近一次修改的日期、时间
        - 第九个字段
            - 文件名
    - chmod
        - `chmod [who] [+|-|=] [permission] 文件或目录名`
        - who: u\g\o\a
    - gzip
        - `$ gzip filename` 压缩文件filename
        - `$ gzip -v file1 file2` 压缩文件file1和file2并显示执行过程
        - `$ gzip -d filename.gz` 解压filename.gz文件
    - zip
    - tar

# Python

## 规范

### 标准库与扩展库中对象的导入和使用

```python
import 模块名 as 别名
from 模块名 import 对象名 as 别名
from 模块名 import *
```
一般建议，每个import语句只导入一个模块，并且要按标准库、扩展库和自定义库的顺序导入

### __name__

__name__这个的话，直接运行程序，这个__name__就是__main__，否则的话，如果是按模块导入的，那就是__name__等于模块名。

我管自己叫我自己，但是在朋友眼里我就是小仙女一样。

### 内置对象

- int 5
- float 3.14
- complex 3 + 2j
- str r'hello'
- bytes b'hello'
- list [1, 2, 3]
- tuple (1, 2)
- dict {1:'food', 2:'tast'}
- set {'a', 'b', 'c'}
- bool True False
- NoneType None
- Exception\ValueError\TypeError...
- 文件 f=open('test.dat', 'rb')
- 其他可迭代对象 range\zip\enumerate\map\filter
- 编程单元 def、class、module

### 常量与变量

这里主要注意命名规范，基本上一样的，不再强调了

### 数字类型

二进制：以0b开头，每一位只能是0或1
八进制：以0o开头.
十六进制：以0x开头

数值的比较请不要用以下方法：
```python
if 0.4 - 0.1 == 0.3:
    print("True")
```
这样不行，你需要这样写：
```python
if abs(0.4 - 0.1 - 0.3) < 1e-6:
    #do sth.
```

### 字符串

```python

s = '''Tom said, "let's go!"'''

```

### 列表、元组、字典、集合

略，稍后写

### 运算符、表达式

+
-
*
/
//
%
**
< <= == >= > !=
or
and
not
in
is
| ^ & << >> ~
& | ^

### 常用内置函数

abs(x)
all(iterable)
any(iterable)
bin(x)
complex(real[, imag])
chr(x)
dir(obj)
enumerate(iterable[, start])
eval(s[, globals[, locals]])
filter(func, seq)
float(x)
globals()
help(obj)
hex(x)
id(obj)
input([tips])
isinstance(obj, class-or-type-or-tuple)
len(obj)
list([x])
set([x])
tuple([x])
dict([x])
locals()
map(func, *iterables)
max(...)
min(...)
next(iterator[, default])
oct(x)
open(name[, mode])
ord(x)
print(value, ..., sep='', end='', file=sys.stdout, flush=False)
range([start,] end[, step])
reduce(func, seq[, initial])
reversed(seq)
round(x[, 小数位数])
sorted(iterable, key=None, reverse=False)
str(obj)
sum(x, start=0)
type(obj)
zip(seq1[, seq2[...]])

### 关键字

False
True
None
and
as
assert
break
class
continue
def
del
elif
else
except
finally
for
from
global
if
import
in
is
lambda
nonlocal
not
or
pass
raise
return
try
while
with
yield

### 列表

append(x)
extend(L)
insert(index, x)
remove(x)
pop([index])
index(x)
count(x)
reverse()
sort(key=None, reverse=False)

列表推导式：
```python

xList = [x+x for x in range(30)]

```
切片
```python
[start:end:step]
aList[::]
aList[::-1] #逆序
aList[3:6] # -> from aList[3] to aList[5]
aList[len(aList):] = [9] # 在列表尾部新增元素
aList[:0] = [9] # 在列表头部新增元素
aList[3:3] = [9] # 在列表中间插元素
aList[:3] = [] # 删除列表前三个元素
```

### 元组

- 如果元组只有一个元素，则必须加一个逗号，如 `a = (1,)` 这样的
- 



