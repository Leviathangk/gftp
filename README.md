# ftp

一个 ftp 下载器

包含 ftp 连接与下载器的方法

- GFTP：新增 FTP 没有的方法
- FTPConn：FTP 连接创建、快速重连
- FTPDownloader：FTP 文件、文件列表、文件夹下载

# 安装

```
pip install gftp
```

# GFTP

新增了一些 FTP 没有的方法

- show_dir：列表形式返回文件夹下的所有文件、文件夹
- show_file：列表形式返回当前文件夹下的所有文件
- show_folder：列表形式返回当前文件夹下的所有文件夹
- iter_dir：遍历指定路径下的文件、文件夹并输出（迭代器）

这里就介绍下 iter_dir

```
from gftp import GFTP

ftp = FTPConn(**连接配置)
for f in ftp.connection.iter_dir('/'):
    print(f)
```

# FTPConn

创建连接用

```
from gftp import GFTP

ftp = FTPConn(**连接配置)
ftp.connection.pwd()    # 通过 connection 使用 FTP 命令
ftp.reconnection()      # 重新连接
ftp.close()             # 关闭连接，会自动回收，关不关无所谓
```

# FTPDownloader

下载文件、文件列表、文件夹  
可以多线程，即创建多个连接  
只提一个参数：keep_structure 会在 save_path 的基础上，保留 ftp 目录结构

```
downloader = FTPDownloader(**连接配置, save_path='')
downloader.download_file()
downloader.download_list()
downloader.download_dir()
```