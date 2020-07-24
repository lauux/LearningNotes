# Linux实战技能100讲-学习笔记



## 系统操作

### 帮助命令

#### `man ` 



#### `help`



#### `info`



### `pwd`



### `ls`

```shell
ls -R dir				# 递归查看dir中的所有文件，包括dir里所有目录下的文件
```





### `cd`

```shell
cd 						# 进入主目录（一般是/home）
cd /					# 进入根目录（/ 即根目录）
cd ..					# 进入当前目录的父级目录
cd ../				# 同上
cd .					# 进入当前目录
cd ./					#	同上
cd -  				#	回到之前操作的目录

```



### 目录相关

#### 创建目录 `mkdir`

无法创建已有的目录

```shell
mkdir [options] [director...]			# 可以同时创建多个目录
mkdir a														# 在当前目录下创建名为a的目录
mkdir ./a													# 同上
mkdir b c d												# 在当前目录下创建分别名为b, c, d的三个目录
```

可以创建多级目录

```shell
mkdir -p a/b/c/d									# 若a b c d 目录不存在，则自动创建
```

#### 删除目录 `rmdir`

只能删除空目录

```shell
rm -r a														# 删除目录 a 无论其是否为空，有提示
rm -r -f a												# 删除目录 a，无提示
rm -rf a													# 与上等价
```

