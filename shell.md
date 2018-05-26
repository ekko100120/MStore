## Shell store
****

1. 修改mac的配置使得vim可以使用系统的复制粘贴[command+c];
```shell
# 在.vimrc配置文件中添加
$ vim ~/.vimsrc
.vimsrc文件中添加:
vmap <C-x> :!pbcopy<CR>   
vmap <C-c> :w !pbcopy<CR><CR>

```
2. vim 操作

vim一共有4个模式：

正常模式 (Normal-mode)  esc+esc
插入模式 (Insert-mode)  i,I,a,A
命令模式 (Command-mode) :
可视模式 (Visual-mode)  先正常模式，然后 v
