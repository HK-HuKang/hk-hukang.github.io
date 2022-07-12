#### 1. tar

tar命令：用途比较多，可以用于打包，也可以用于压缩和解压缩

**打包和压缩的区别**

打包：将一堆文件或目录编程一个文件

压缩：将一个大文件，通过压缩算法变成一个小文件

Linux中的很多压缩算法只能对一个文件进行压缩，所以我们要压缩的话，必须先进行打包

tar命令加或不加 **-** 都可以

**常用的压缩算法**

gzip、 bzip2、 xz等

一下5个选项不能连用

**-c**：创建一个打包文件

**-x**：解开一个压缩文件

**-t**：查看压缩文件的内容

**-r**：在一个归档的文件的末尾添加一个文件

**-u**：更新源压缩包中的文件



**以下3个选项问常用的压缩方式**

**-z**：使用gzip压缩

**-j(小写)**：使用bzip2压缩

**-J（大写）**：使用xz压缩



**一下1个选项为必须参数**

**-f**：该选项必须写在最后，后面接文件名



**常用选项**

**-v**：显示压缩或解压缩的过程

-**C(大写)**：后面接要解压到的目录



**配置举例**

**压缩**

```shell
tar -cvf boot.tar /boot
把/boot目录打包为boot.tar，打包后的文件，我们习惯使用.tar

tar -zcvf boot.tar.gz /boot
把/boot目录打包并且压缩为gzip格式，命名为boot.tar.gz，gzip压缩的文件，我们习惯加一个gz

tar -jcvf boot.tar.bz2 /boot
把/boot目录打包并且压缩为bzip2格式，命名为boot.tar.bz2，bzip2压缩的文件，我们习惯加一个bz2
```





**查看压缩文件的内容**

```shell
tar -tf boot.tar.bz2
```





**解压文件**

直接解压

```shell
tar xvf boot.tar	//直接解压tar包
tar xzvf boot.tar.gz	//解压gzip2文件
```

要解压到特定的目录，需要切换到该目录下，不能后面直接写目录

**注意：这一点有问题，可以直接用 -C 选项加目录**

```shell
cd /tmp/Maidao
tar xjvf /tmp/boot.tar.bz2
```



解压到特定目录

```shell
tar -xzvf boot.tar.gz -C /home/kang/test/
解压到指定目录
```

只想解压/boot/grup2/grub.cfg 文件

```shell
tar xzvf /tmp/boot.tar.gz boot/grub2/grup.cfg
注意：boot/grup2/grup.cfg	内的根目录 / 是被拿掉的
```

在打包压缩时排除某一个文件

```shell
tar --exclude /boot/grub/splash.xmp.gz -zcvf boot2.tar.gz /boot
```



**补充**：Windows中的zip和rar格式也适用于Linux

​			**zip**和**rar**命令可以对文件或目录进行**zip**或**rar**压缩

​			**unzip**和**unrar**命令可以对文件或目录进行**zip**或**rar**压缩





#### 2. zip&unzip

原教程地址([Linux zip&unzip命令 | idev365](https://www.idev365.com/linux/cmd-backup/))

视频教程(https://b23.tv/DaGqz66)

**压缩文件**

```shell
zip archive inpath inpath ...
```

- **archive**  指定生成归档文件的路径
- **inpath inpath ...**  要添加到压缩包中的文件路径

eg:

```shell
zip back.zip test/*.txt
//将text中的txt文件压缩为back.zip
```

**分卷压缩**

```shell
zip -s 64k new.zip *.txt
```

- **-s 64k**   指定分卷大小为64k, zip允许的最小分卷大小为64k

```shell
zip text.zip /bin/zsh -s 100k
```

- 将/bin/zsh 作为分卷压缩的对象，生成100k为分卷大小的压缩包



对压缩包重新分卷，如果你有一个较大的压缩包，要进行分卷也可以采用类似的方法

```shell
zip big.ziph --out new.zip -s 1m
```



**zip的更多参数**

| 参数 | 说明                                                |
| ---- | --------------------------------------------------- |
| -r   | 递归遍历目录                                        |
| -q   | 不显示压缩命令的执行过程（q为quit的缩写，安静模式） |
| -d   | 删除压缩包中指定文件                                |

```shell
zip -r backup2.zip test

zip backup3.zip test

对比不适应 -r 的差异
```

- 不使用`-r`参数，压缩遇到目录，只会添加目录路径本身，不会遍历目录内其他文件

**从压缩包中删除指定的文件**

```shell
zip -d backup2.zip  test/abc.txt
```



**解压缩文件**

```shell
unzip filepath
```

- `filepath` 要解压缩的文件的路径。

**unzip的更多参数**

```shell
unzip file -d exdir
```

- `file`要解压缩的文件路径
- `-d exdir`指定要解压缩的路径，其中`exdir`为解压缩后的文件路径

```shell
unzip backup.zip -d /home/abc
```

 **unzip参数小结**

| 参数   | 说明           |
| ------ | -------------- |
| **-v** | 查看压缩包内容 |
| **-d** | 指定解压缩路径 |

