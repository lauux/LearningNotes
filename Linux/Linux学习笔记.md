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

##### 打包、压缩 

最早的 Linux 备份介质是磁带，使用的**打包命令**是 `tar`

打包后的磁带文件可以进行压缩存储，**压缩命令**是 `gzip` 和 `bzip2`

经常使用的扩展名是 `.tar.gz`, `.tar.bz2`, `.tgz`

```shell
# 打包
tar cf /tmp/etc-backup.tar /etc 	# 将/etc目录打包，放至/tmp目录下，并命名为etc-backup.
# tar常见参数
	# c 打包
	# x 解包
	# f 指定操作类型为文件

# 压缩
gzip 
bzip2
# 打包并压缩 bzip2 比 gzip 速度慢
tar czf /tmp/etc-backup.tar.gz /etc
tar cjf /tmp/etc-backup.tar.bz2 /etc	
```

##### 解压缩

```shell
tar xf /tmp/etc-backup.tar -C /root	# 将/tmp下的etc-backup.tar解压缩并放至/root下
tar zxf # ...												# 解压 .tar.gz 即.tgz
tar jxf # ...												# 解压 .tar.bz2 即.tbz2
```



### Vim 编辑器

#### 四种模式

##### 正常模式（Normal-mode）

默认进入时的模式

- **方向控制：**

`hjkl` 分别为左下上右

- **文本操作：**

`yy` 整行复制

`nyy` 复制当前及后面共n行，n为具体数字

`y$` 复制光标至当前行尾的内容

`dd` 整行剪切

`d$` 剪切光标至当前行尾的内容

`p` 键粘贴

`u` 撤销

`ctrl r` 重做

`x`  删除单个字符

`ra` 将光标当前内容替换为a（a为任意想替换的字符）

- **光标移动：**

`g` 光标移动到文本首行

`G` 光标移动到文本末行

`^`  光标移至行首

`$ 光标移至行尾`

##### 插入模式（Insert-mode）

文本输入的模式

`i` 键进入光标当前位置前方，`I` 光标移动到当前行头

`a` 键进入光标当前位置后方，`A` 光标移动到当前行尾

`o` 键进入并在光标下方新建一空行，`O` 在光标上方新建空行

`esc` 退出插入模式，进入正常模式

##### 命令模式（Command-mode）

也可以叫末行模式（命令显示在底部）

在正常模式下按 `:` 键可**进入命令模式**并输入命令

`w /root/test.txt` 保存至`/root` 目录下并命名为 text.txt，单键入`w` 则保存到现有文件

`q` 退出文件（保存后）

上述两个命令可以一起用 `wq` 保存并退出

`q!` 强制退出（不保存）

`!command` 执行command（任意的linux可执行）命令

`set nu` 显示行号（单次有效，若要长期有效需要在配置文件vimrc中修改）

`set nonu`  不显示行号

- **查找**

`/x` 查找 “x”，若有多个"x"，可以通过 `n` 键切换到下一个，`N` 即 `<shift>n` 切换到上一个

- **替换**

`s/old/new` 将当前行中第一次出现的old替换成new

`%s/old/new` 将全文中第一次出现的old替换成new

`1,12s/old/new` 将1到12行中第一次出现的old替换成new

上述命令末尾加上`/g` 则是全部（global），即

`1,12s/old/new/g` 将1到12行中所有出现的old替换成new

##### 可视模式（Visual-mode）

- 三种进入方法
  - `v` 字符可视模式
  - `V` 行可视模式
  - `<ctrl> v` 块可视模式（配合 `d` 和 `I` 命令可进行块的便利操作）



### 用户与权限管理

#### 用户管理

##### 新建用户 `useradd`

```shell
useradd newUser										# 新建名为 newUser 的用户
id userName												# 查询用户 userName
```

**新建用户后**：

会在 `/home` 目录下新建同名用户家目录

同时新用户会被记录在 `/etc/passwd` 和 `/etc/shadow` 中（用户密码习惯文件）

会给新用户分配 `uid` ，root用户的 `uid` 一般是 `0`

会创建同名的用户组（进行资源限制，对一组进行权限修改则会影响到该组所有成员）

##### 删除用户 `userdel`

```shell
userdel userName									# 删除名为 userName 的用户
userdel -r userName								# 删除 userName 用户及其对应的记录（/home 目录，passwd记录等）
```

##### 修改用户密码 `passwd`

```shell
passwd userName 									# 为用户 userNme 创建/更改密码
passwd														# 为自己（root）修改密码
```

##### 修改用户信息 `usermod`

```shell
usermode [options] userName				# 修改用户信息
usermode -d /home/newname oldname	# 修改用户家目录
```

##### 修改用户密码过期时间 `chage`

```shell
chage [options] userName
```

##### 切换用户 `su`

```shell
su - userName											# 当前用户切换为 userName，并同时更改运行环境（- 的作用）
```

`root` 用户切换到其他用户无需输入密码，其他则需要

##### 以其他用户身份执行命令 `sudo`

```shell
visudo 														# 授权能够使用 sudo 的用户
######### visudo 文件内
userName ALL=/path/command				# 授权用户 userName 在任何界面（图形/字符终端）执行 command 命令
%group localhost=/path/command		# 授权组 group 内的所有用户在字符界面执行 command 的命令
```



#### 组管理

##### 新建用户组 `groupadd`

```shell
groupadd newGroup								# 新建用户组 newGroup
useradd newUser									# 新建用户 newUser
usermod -g newGroup newUser			# 将 newUser 添加进 newGroup 组内

useradd -g newGroup newUser2		# 新建用户 newUser2 并将其添加进 newGroup 组内
```

##### 删除用户组 `groupdel`

```shell
groupdel groupName							# 删除用户组 groupName
```



#### 配置文件

##### 用户属性配置文件 `/etc/passwd`

```shell
##### /etc/passwd 配置文件内
# 格式 userName:是否需要密码验证（x即是，空即否）:uid:gid:注释:/家目录:命令解释器
root:x:0:0:root:/root:/bin/bash
user1:x:1001:1001::/home/user1:/bin/bash
tcpdump:x:72:72::/:/sbin/nologin # 不允许该用户在终端登录
```

可以通过修改该文件内容添加新用户，但是当所指定的用户家目录不存在时，则无法分配其家目录，且命令解释器只显示版本号（通过 `id` 查询时）

##### 用户密码信息文件 `/etc/shadow`

```shell
##### /etc/shadow 配置文件内
# 格式 userName:用户密码密文（相同的密码也不一定相同）:...
```

##### 用户组配置文件 `/etc/group`

```shell
##### /etc/group 配置文件内
# 格式 groupName:是否需要密码验证:gid:其他组设置
root:x:0:
mail:x:12:postfix # postfix 同时属于 组postfix 和 组mail
```



#### 文件权限

```shell
-rw------- 1 user group 1523 apr 9 20:19 fileName
# 类型:-（普通文件）
# 权限:通常有r/w/x 位置相关-前三（所属用户对该文件的的权限）中三（用户组成员对该文件的的权限）后三（其他用户对该文件的权限）
# 所属用户和组: 用户user 组group
# 文件名: fileName
```

创建新文件有默认权限，根据 `umask` 值计算（`666-`umask的值），属主和属组根据当前进程的用户来设定

##### 文件类型

`-` 普通文件

`d` 目录文件

`b` 块特殊文件（例如：设备）

`c` 字符特殊文件

`l` 符号链接

`f` 命名管道

`s` 套接字文件

##### 文件权限的表示方法

- **字符权限表示方法**
  - `r` 读
  - `w` 写
  - `x` 执行
- **数字权限表示方法（八进制）**
  - r = 4
  - w = 2
  - x = 1

##### 目录权限的表示方法

`x` 进入目录

`rx` 显示目录内的文件名

`wx` 修改目录内的文件名

##### 修改权限命令

 **`chmod`** 修改文件、目录权限

```shell
# u-属主 g-属组 o-其他 a-所有
# +增加权限 -减少权限 =设置权限
chmod u+x /tmp/testfile						# 为属主增加对/tmp/testfile 文件的执行权限
# 每个位置对应 属主 属组 其他
chmod 755 /tmp/testfile


```

**`chown`** 更改属主、属组

```shell
chown userName fileName 					# 将文件/目录 fileNme 的属主更改为用户userName 
chown :groupName fileName					# 将文件/目录 fileNme 的属组更改为用户组groupName
chown user:group fileName					# 同时修改文件/目录 fileNme 的属主和属组
```

**`chgrp`** 可以单独更改属组，不常用

```shell
chgrp groupName fileName					# 将文件/目录 fileNme 的属组更改为用户组groupName
```



#### 权限管理及特殊权限

##### 权限管理

- 若属主和属组的**权限冲突，以属主权限为准**。如属主无 `w` 权限，即使属主所在的组有 `w` 权限，属主也无法进行写操作

- 若对目录只有 `r` 权限没有 `x` 权限，则无法看到目录内的相关信息，但是可以查看目录内的文件名

  ```shell
  [root]  chmod 400 /test
  [user1] ls -l /test
  ls: cannot access /test/afile: Permission denied
  ls: cannot access /test/bfile: Permission denied
  total 0
  -????????? ? ? ? ?				? afile
  -????????? ? ? ? ?				? bfile
  # 也无法进入
  bash: cd: test: Permission denied
  ```

- 若对目录只有 `x` 权限，则可以进入该目录，但无法查看目录内的所有文件（可以指定一个文件查看）

  ```shell
  [user@ /]     cd /test # 可以进入
  [user1@/test] ls -l 
  ls: cannot access /test/bfile: Permission denied
  [user1@/test] ls -l afile
  -rw-r--r--. 1 root root 0 Jul 29 04:20 afile
  ```

- 若对目录有 `wx` 权限，则可以进入该目录，但是无法查看目录下的文件，且对目录可以进行删除 `rm` 前提是目录下的文件是当前用户有权限的，否则无法删除

##### 特殊权限

- `SUID` 用于二进制可执行文件，执行命令时取得文件属主权限

  - 如 `/usr/bin/passwd`

    ```shell
    ls -l /usr/bin/passwd
    -rwsr-xr-x. 1 root root #... 后部分省略
    # 即无论是哪个用户，对该文件操作时都视作属主 root
    ```

- `SGID` 用于目录，在该目录下创建新的文件和目录，权限自动更改为该目录的属组

- `SBIT` 用于目录，该目录下新建的文件和目录，仅 `root` 和自己可以删除

  - 如 `/tmp`

    ```shell
    ls -ld /tmp/
    drwxrwxrwt. 16 root root #... 后部分省略
    # 防止其他用户误删文件
    ```

**添加特殊权限**

不建议添加或更改特殊权限

```shell
# set SUID
chmod 4xxx target 								# xxx为target原有权限

[root] chmod 4755 /test/bfile
[root] ls -l /test/bfile
-rwsr-xr-x. 1 user1 group1 #...

# set SBIT
chmod 1xxx target
```



----



## 系统管理











----



### 通配符

```shell
*																	# 匹配任意长度的任意字符
?																	# 匹配一个长度的任意字符
```





