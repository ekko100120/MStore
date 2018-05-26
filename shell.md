## Shell store
****

##### 1. 修改mac的配置使得vim可以使用系统的复制粘贴[command+c];
```shell
# 在.vimrc配置文件中添加
$ vim ~/.vimsrc
.vimsrc文件中添加:
vmap <C-x> :!pbcopy<CR>   
vmap <C-c> :w !pbcopy<CR><CR>

```
##### 2. vim 操作

vim一共有4个模式：

* 正常模式 (Normal-mode)  esc+esc
* 插入模式 (Insert-mode)  i,I,a,A
* 命令模式 (Command-mode) :
* 可视模式 (Visual-mode)  先正常模式，然后 v-->块可视化  shift+v-->行可视化
vim命令
* 删除 d
* 撤销 u
* 复制 光标定位到当前行-->y
* 粘贴 p
* 恢复撤销
* h--i--k--l ---->左-->下-->上-->右

* dd:删除游标所在的一整行(常用)
* ndd:n为数字。删除光标所在的向下n行，例如20dd则是删除光标所在的向下20行
* d1G:删除光标所在到第一行的所有数据
* dG:删除光标所在到最后一行的所有数据
* d$:删除光标所在处，到该行的最后一个字符
* d0:那个是数字0,删除光标所在到该行的最前面的一个字符
* x,X:x向后删除一个字符(相当于[del]按键),X向前删除一个字符(相当于[backspace]即退格键)
* nx:n为数字，连续向后删除n个字符

##### 3 $意义

$$

Shell本身的PID（ProcessID）

$!

Shell最后运行的后台Process的PID

$?

最后运行的命令的结束代码（返回值）

$-

使用Set命令设定的Flag一览

$*

所有参数列表。如"$*"用「"」括起来的情况、以"$1 $2 … $n"的形式输出所有参数。

$@
所有参数列表。如"$@"用「"」括起来的情况、以"$1" "$2" … "$n" 的形式输出所有参数。

$#

添加到Shell的参数个数

$0

Shell本身的文件名

$1～$n

添加到Shell的各参数值。$1是第1参数、$2是第2参数…。

###### 获取当前文件的工作目录,当前脚本名
```shell
$ workdir=$(cd $(dirname $0); pwd)
#获取当前脚本名
$ basename $0
```
##### 打印奇数行偶数行
$ awk "NR%2" filename #答应奇数行
$ awk "!(NR%2)" filename #打印偶数行


