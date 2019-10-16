# 在线监测系统维护手册 服务器

![stars](https://img.shields.io/github/stars/haithing/manual?style=social)
![watchers](https://img.shields.io/github/watchers/haithing/manual?style=social)
![latest release](https://img.shields.io/github/v/release/haithing/manual?style=social)
![file size](https://img.shields.io/github/repo-size/haithing/manual?style=social)

## 前言

本手册采用 Markdown 编制，托管于 Github 。
本手册致力于做到 _覆盖面广_（涉及所有重要的内容），_具体_（给出具体的最常用的例子），以及 _简洁_（避免冗余的内容，或是可以在其他地方轻松查到的细枝末节）。
熟练的掌握本手册所述内容能帮助你节约大量的时间。

### 在线查阅 ![release date](https://img.shields.io/github/release-date/haithing/manual)

-   本手册在不断的充实完善，建议关注后在线查阅。你的支持也是我们进步的动力。

-   :link: https://github.com/haithing/manual

### 反馈建议 ![issues](https://img.shields.io/github/issues/haithing/manual)

-   如果你在本手册中发现了错误或者存在可以改善的地方，请贡献你的一份力量。

-   :link: https://github.com/haithing/manual/issues

### 下载手册 ![downloads](https://img.shields.io/github/downloads/haithing/manual/total)

-   本手册提供了 pdf 、 word 等多种版本供下载后查阅，请随时关注更新并获取最新的版本。

-   :link: https://github.com/haithing/manual/releases/latest

### 版本记录

| 版本号 |  修订时间  | 修订说明                  |
| :----: | :--------: | ------------------------- |
|  v0.1  | 2019/10/15 | 开始编写手册              |
|  v0.2  | 2019/10/15 | 添加维护 Linux 服务器章节 |

## 维护 Linux 服务器

<img src="files/linux.svg"  />

阀厅项目服务器使用的是 Linux 系统，我们通过 _终端 (Terminal)_ 来和他进行交互。
在 Linux 系统上可以通过按 **Ctrl+Alt+T** 快捷键打开终端。
在 Windows 系统上我们需要安装终端软件，常用的终端软件有 xshell 、 git 、 putty 等。

本章节将介绍终端的基本使用，下文中 `终端` 泛指上述软件中的任意一个。

### 常用终端

#### xshell

<img src="files/xshell.png" width="80" />

-   :link: http://server.haithing.com/ois/windows/support/xshell.exe `(内网)`

-   xshell 是收费软件，需注意试用期问题。

-   安装后通过桌面快捷方式打开软件。

#### git

<img src="files/git.png" width="80" />

-   :link: https://www.git-scm.com/download

-   安装后在桌面点右键，选择 `Git Bash Here` 打开软件。

### 操作技能

熟悉以下操作技能可以让你在操作时事半功倍，还让你显得很酷 :sunglasses: 。

#### 自动补全

按 **Tab** 键实现自动补全参数。自动补全不仅能有效提高输入效率，还可以 _避免输入错误_ :100: 。

请参阅以下示例（ `→` 表示 **Tab** 键）练习。

```bash
cd /var/www/media/log/
cd /v→w→m→l→

sz server.log
sz s→

history
his→
```

#### 快捷键

|           按键           |          操作          |
| :----------------------: | :--------------------: |
|        **Ctrl+C**        |        中断操作        |
|     **Ctrl+Insert**      |          复制          |
|     **Shift+Insert**     |          粘贴          |
| **Ctrl+P**（或向上箭头） |   获取前一个历史命令   |
| **Ctrl+N**（或向下箭头） |   获取后一个历史命令   |
| **Ctrl+B**（或左箭头键） |   将光标回退一个字符   |
| **Ctrl+F**（或右箭头键） |   将光标前进一个字符   |
|        **Ctrl+A**        |     移动光标至行首     |
|        **Ctrl+E**        |     移动光标至行尾     |
|        **Ctrl+K**        |   删除光标之后的内容   |
|        **Ctrl+U**        |   删除光标之前的内容   |
|        **Ctrl+W**        | 删除光标之前的一个单词 |
|        **Ctrl+Y**        |   恢复之前删除的内容   |
|        **Ctrl+T**        |   交换前两个字符位置   |
|        **Ctrl+L**        |          清屏          |

#### 系统时间

-   使用 `date` 命令来查看系统时间，`date +%s` 查看时间戳， `date +%F\ %T` 可以让输出的时间更直观。

-   使用 `date -d @时间戳` 可以解析时间戳。

-   使用 `date -s 时间` 可以设置系统时间。

-   使用 `uptime` 或 `w` 命令来查看系统运行时间。

```bash
$ date -s 10:00:00
2019年 10月 01日 星期二 10:00:00 CST
$ date
2019年 10月 01日 星期二 10:00:00 CST
$ date +%s
1569895200
$ date -d @1569895200
2019年 10月 01日 星期二 10:00:00 CST
$ date -d @1569895200 +%F\ %T
2019-10-01 10:00:00
```

#### 更多

-   可以打开多个 `终端`  来进行不同的操作。

-   使用 `history` 命令查看历史记录，输入 `!n`（`n` 是命令编号）就可以再次执行。

-   使用 `ifconfig` 命令获取网络连接状态。

-   使用 `top` 命令获取 CPU 和硬盘的使用状态。

-   使用 `df -h` 命令查看硬盘的使用。

-   使用 `sudo reboot` 命令重启服务器。

### 连接到服务器

> 请勿在 xshell 中保存服务器密码。

打开 `终端` ，输入命令 `ssh 用户名@服务器`（如 `ssh hs@192.168.8.2`），回车，输入密码，出现 `Welcome to XXX` 信息即已成功连接服务器。

-   服务器 ip 地址与客户端网页地址一致，阀厅项目通常为 `192.168.8.2` 。

-   用户名通常为 `hs` 。

-   在 `终端` 输入密码时无任何反馈，且输入错误无法删除。

### 目录操作

-   目录层级用 `/` 分隔。

-   用 `cd` 命令切换工作路径，输入 `cd ~` 可以进入 home 目录。要访问你的 home 目录中的文件，可以使用前缀 `~`（例如 `~/server`）。输入 `cd -` 回到前一个工作路径。

-   用 `pwd` 命令查看当前目录。

-   绝对路径从根目录（`/`）开始，如 `/var/www/html` 。

-   相对路径从当前目录开始，`.` 表示当前目录， `..` 表示当前目录的上层目录。

```bash
$ cd /var/www/html && pwd
/var/www/html
$ cd ../media && pwd
/var/www/media
$ cd ./picture && pwd
/var/www/media/picture
$ cd ../../media/report && pwd
/var/www/media/report
```

#### 常用目录

| 目录                     | 说明             |
| ------------------------ | ---------------- |
| `/var/www/media/log`     | 日志存放目录     |
| `/var/www/media/report`  | 报表存放目录     |
| `/var/www/media/picture` | 图片存放目录     |
| `/var/www/media/video`   | 视频存放目录     |
| `/var/www/html`          | 网页工作目录     |
| `~/server`               | 服务程序工作目录 |

### 上传下载文件

#### scp

打开 `终端` （无需连接到服务器），输入如下命令：

```bash
scp [源主机]:[源文件] [目标主机]:[目标路径]

## 示例

## 上传报表生成脚本
scp default.php hs@192.168.8.2:/var/www/media/report

## 下载服务端日志
scp hs@192.168.8.2:/var/www/media/log/server.log ./
```

#### lrzsz

使用 lrzsz 前需通过 xshell 连接到服务器。

**sz**

-   将选定的文件下载到本地。

**rz**

-   运行该命令会弹出一个文件选择窗口，从本地选择文件上传到服务器。

-   如果服务器上存在同名文件，需先删除。

### 编辑配置文件

#### 在服务器上编辑

1. 输入 `vim [filename]` 开始编辑。

1. 按 **i** 进入编辑模式。

1. 编辑配置文件。

1. 按 **Esc** 退出编辑模式。

1. 按 **Shift+;** 进入命令行模式。

    - 输入 `w` 保存文档。

    - 输入 `q` 退出文档。

    - 输入 `wq` 保存并退出文档。

#### 下载到本地后编辑

通过 '上传下载文件' 所述方法下载配置文件到本地，编辑后上传到服务器。
本地编辑时请注意保持换行符为 `LF` 。

<img src="files/vscode.png" width="80" />

推荐使用 [:link: Visual Studio Code](https://code.visualstudio.com) 进行本地编辑。
