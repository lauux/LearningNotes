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



### 目录/文件相关

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

#### 复制 `cp`

```shell
cp [options] source_file target_file
cp /root/a/afile /root/b/bfile 		# 复制/root/a目录下的afile文件到/root/b目录下并更名为bfile
cp -r /root/a /tmp 								# 将/root/a目录复制到/tmp中
cp -r /root/a /tmp/b							# 若tmp中不存在名为b的目录，则将目录/root/a复制到/tmp中并更名为b
cp -v /root/a/afile /root/b				# 复制，不更名，并显示过程
cp -p	source_file targetfile			# 保留原有时间，属主状态
cp -a	source_file targetfile			# 保留原有时间，属主，权限
```

#### 移动 `mv` （可用于文件重命名）

```shell
mv [options] source target
mv /root/a/afile /tmp 						# 将/root/a目录下的afile文件移动到/tmp中
mv /root/a/afile /root/b/bfile 		# 将/root/a目录下的afile文件移动到/root/b目录下并更名为bfile
mv ./afile ./bfile								# 将当前目录下的afile重命名为bfile	
```

#### 文本查看

##### `cat `文本内容显示到终端

```shell
cat /demo
```

##### `head` 查看文件开头

```shell
head /demo
head -5 /demo											# 显示前5行
```

##### `tail` 查看文件结尾

常用参数 `-f` 文件内容更新后，显示信息同步更新

```shell
tail /demo
tail -5 /demo											# 显示后5行
tail -f /demo											# 若demo是实时变化，则会同步更新到终端，用ctrl+c退出
```

##### `wc` 统计文件内容信息

```shell
wc -l /demo												# 显示文件行数
```

##### `more` , `less` 分页显示

```shell
more /demo												# 只能向后翻页，不能向前翻页
less /demo												# 能前后翻页
```

#### 打包压缩和解压缩







### 通配符

```shell
*																	# 匹配任意长度的任意字符
?																	# 匹配一个长度的任意字符
```





