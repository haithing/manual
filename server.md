# 在线监测系统服务器运维手册

## 目录

[TOC]

## 前言

![stars](https://img.shields.io/github/stars/haithing/manual?style=social)
![watchers](https://img.shields.io/github/watchers/haithing/manual?style=social)
![latest release](https://img.shields.io/github/v/release/haithing/manual?style=social)
![file size](https://img.shields.io/github/repo-size/haithing/manual?style=social)
![license](https://img.shields.io/github/license/haithing/manual?style=social)

本手册供我司在线监测系统服务器运维人员使用。

本手册致力于做到
_覆盖面广_（涉及所有重要的内容），
_具体_（给出具体的最常用的例子），
_简洁_（避免冗余的内容，或是可以在其他地方轻松查到的细枝末节）。
熟练的掌握本手册所述内容能帮助你节约大量的时间。

本手册使用 MIT 开源协议，欢迎大家贡献自己的内容 。

### 在线查阅 ![release date](https://img.shields.io/github/release-date/haithing/manual)

-   本手册在不断的充实完善，建议关注后在线查阅。你的支持也是我们进步的动力。

-   :link: https://github.com/haithing/manual

### 反馈建议 ![issues](https://img.shields.io/github/issues/haithing/manual)

-   如果在本手册中发现了错误或者存在可以改善的地方，请贡献你的一份力量。

-   :link: https://github.com/haithing/manual/issues

### 下载手册 ![downloads](https://img.shields.io/github/downloads/haithing/manual/total)

-   本手册提供了 pdf 、 word 等多种版本供下载后查阅，请随时关注更新并获取最新的版本。

-   :link: https://github.com/haithing/manual/releases/latest

### 版本记录

| 版本号 |  修订时间  | 修订说明                    |
| :----: | :--------: | --------------------------- |
|  v0.1  | 2019/10/15 | 开始编写手册                |
|  v0.2  | 2019/10/15 | 添加 Linux 服务器运维章节   |
|  v0.3  | 2019/10/16 | 添加 Windows 服务器运维章节 |
|  v0.4  | 2019/10/18 | 添加常见问题章节            |
|  v0.5  | 2019/10/21 | 添加系统配置与操作章节      |

## Linux 服务器运维

<img src="files/ubuntu.svg" width="80" />

我司项目服务端选用 Ubuntu 16.04 LTS 发行版。
本手册所述流程及所列示例均基于此发行版。

本章节基于 _理论够用、侧重实用_ 的原则来说明 Linux 服务器的基本运维操作。

### 终端

我们通过 **终端（Terminal）** 来和装载有 Linux 系统的服务器进行交互。
在 Linux 系统上可以通过 <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>T</kbd> 快捷键打开终端。
在 Windows 系统上我们需要额外安装终端软件来远程登录到服务器。
常见的终端软件有 Xshell 、 Git 、 Termius 、 SecureCRT 、 PuTTY 等。

**_Xshell_**

<img src="files/xshell.png" width="80" />

-   请在 [附录 - 常用软件](#xshell) 获取下载链接。

-   Xshell 是收费软件，需注意试用期问题。

-   安装后通过桌面快捷方式打开软件。

**_Git_**

<img src="files/git.png" width="80" />

-   请在 [附录 - 常用软件](#git) 获取下载链接。

-   Git for Windows 使用
    [GPL](https://github.com/git-for-windows/git)
    开源协议，我们可以免费使用。

-   Git for Windows 的功能十分强大，我们仅使用其中一小部分功能。

-   安装后在桌面点右键，选择 `Git Bash Here` 打开软件。

**_Termius_**

<img src="files/termius.png" width="80" />

-   请在 [附录 - 常用软件](#termius) 获取下载链接。

-   Termius 支持 Windows 、 Linux 以及 macOS 等平台，也支持在 Android 和 iOS 上使用。

-   Termius 的免费功能已足够我们的使用。

-   安装后通过桌面快捷方式打开软件。

下文中 **终端** 泛指上述软件中的任意一个。

### 操作技能

熟悉以下操作技能可以让你在操作时事半功倍，还让你显得很酷 :sunglasses: 。

#### 自动补全

按 <kbd>Tab</kbd> 键实现自动补全参数。
自动补全不仅能有效提高输入效率，还可以 _避免输入错误_ :100: 。

请参阅以下示例（ `→` 表示 <kbd>Tab</kbd> 键）练习。

```bash
cd /var/www/media/log/
cd /v→w→m→l→

sz server.log
sz s→

history
his→
```

#### 快捷键

|           按键            |         操作         |            按键            |        操作        |
| :-----------------------: | :------------------: | :------------------------: | :----------------: |
|        **Ctrl+C**         |       中断操作       |         **Ctrl+L**         |        清屏        |
|      **Ctrl+Insert**      |         复制         |      **Shift+Insert**      |        粘贴        |
|  :arrow_up: / **Ctrl+P**  |  获取前一个历史命令  | :arrow_down: / **Ctrl+N**  | 获取后一个历史命令 |
| :arrow_left: / **Ctrl+B** |  将光标回退一个字符  | :arrow_right: / **Ctrl+F** | 将光标前进一个字符 |
|   **Home** / **Ctrl+A**   |    移动光标至行首    |    **End** / **Ctrl+E**    |   移动光标至行尾   |
|        **Ctrl+U**         |   移除光标前的内容   |         **Ctrl+K**         |  移除光标后的内容  |
|        **Ctrl+W**         | 移除光标前的一个单词 |         **Ctrl+Y**         |   恢复移除的内容   |
|        **Ctrl+T**         |  交换前两个字符位置  |                            |                    |

#### 更多

-   可以打开多个 **终端** 来进行不同的操作。

-   使用 `history` 命令查看历史记录，输入 `!n` （ `n` 是命令编号）就可以再次执行。

-   使用 `sudo reboot` 命令重启服务器。

### 连接到服务器

> 请勿在 xshell 中保存服务器密码。

打开 **终端** 。
输入命令 `ssh 用户名@服务器` ， 如 `ssh hs@192.168.8.2` 。
输入正确的密码，出现 `Welcome to XXX` 信息即已成功连接到服务器。

-   服务器 ip 地址与客户端网页地址一致，
    阀厅项目通常为 `192.168.8.2` 。

-   用户名通常为 `hs` 。

-   在 **终端** 输入密码时无任何反馈，且输入错误无法删除。

### 目录操作

-   目录层级用 `/` 分隔。

-   用 `cd` 命令切换工作路径。
    直接输入 `cd` 进入当前用户的家目录。
    输入 `cd -` 回到前一个工作路径。

-   用 `pwd` 命令查看当前目录。

-   绝对路径从根目录（ `/` ）开始，如 `/var/www/html` 。
    `~` 表示当前用户的家目录，如 `~/server` 。

-   相对路径从当前目录开始。
    `.` 表示当前目录。
    `..` 表示当前目录的上层目录。

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

| 说明             | 目录                     |
| ---------------- | ------------------------ |
| 日志存放目录     | `/var/www/media/log`     |
| 报表存放目录     | `/var/www/media/report`  |
| 图片存放目录     | `/var/www/media/picture` |
| 视频存放目录     | `/var/www/media/video`   |
| 网页工作目录     | `/var/www/html`          |
| 服务程序工作目录 | `~/server`               |

### 上传下载文件

#### _scp_

在 **终端** （无需连接到服务器）操作。

```bash
# 从本地拷贝文件到服务器
scp source_file user@host:directory/target_file
# 示例：上传报表生成脚本
scp default.php hs@192.168.8.2:/var/www/media/report

# 从服务器拷贝文件到本地
scp user@host:directory/source_file target_file
# 示例：下载服务程序日志
scp hs@192.168.8.2:/var/www/media/log/server.log ./
```

#### _zmodem (lrzsz)_

使用 zmodem 协议前需通过 xshell 连接到服务器。

-   **`rz` 命令** 即 _receive_ ，服务器接收，客户机上传。

    -   运行该命令会弹出一个文件选择窗口，从本地选择文件上传到服务器。

    -   如果服务器上存在同名文件，需先删除。

-   **`sz` 命令** 即 _send_ ，服务器发送，客户机下载。

    -   将选定的文件下载到本地。

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

通过 [上传下载文件](#上传下载文件) 所述方法下载配置文件到本地，编辑后上传到服务器。
本地编辑时请注意保持换行符为 `LF` 。

<img src="files/vscode.png" width="80" />

推荐使用 [Visual Studio Code](#visual-studio-code) 进行本地编辑。

### 系统时间管理

-   使用 `date` 命令来查看系统时间，`date +%s` 查看时间戳， `date +%F\ %T` 可以让输出的时间更直观。

-   使用 `date -d @时间戳` 可以解析时间戳。

-   使用 `date -s 时间` 可以设置系统时间。

```bash
$ date -s 10:00:00
2019年 10月 01日 星期二 10:00:00 CST
$ date +%s
1569895200
$ date -d @1569895200 +%F\ %T
2019-10-01 10:00:00
```

### 系统状态查看

-   使用 `ifconfig` 命令获取网络连接状态。

-   使用 `uptime` 或 `w` 命令来查看系统运行时间。

-   使用 `top` 命令查看进程所占系统资源。

-   使用 `df -h` 命令查看硬盘的使用。

## Windows 服务器运维

部分项目未单独配置服务器，这些项目中客户端也作为服务器使用。

### 配置 Windows 服务器

#### 配置流程

_请严格按配置流程操作，任何遗漏都将引发不可预期的后果。_

_Please strictly follow the configuration process, any of your omissions will lead to unexpected consequences._

1.  请在 Windows 7 或更高版本的操作系统上操作。

1.  在 Windows 10 操作系统上部署本系统服务端时需激活并切换至 **_administrator_** 用户。

    > _以 **管理员身份** 运行命令 `net user administrator /active:yes`_ 。

1.  配置 _用户账户控制（UAC）_ 为 `从不通知` 。

1.  安装 [_支持组件（support.exe）_][support] 到 **_d:\etc_** 目录。

1.  获取 [_安装包_][setup] 并解压至 **_d_** 盘任意位置。

1.  以 **管理员身份** 运行 **_setup.bat_** 执行安装操作。

1.  在 _支持组件_ 中切换版本为 `"php-5.5.38 + Apache"` ，设置运行模式为 `"系统服务"` 。

    ![support](files/support.png)

1.  在 **Internet Explore 11** 浏览器中输入地址 [`http://localhost`](http://localhost) 打开客户端网页。

#### 配置说明

-   服务程序可部署至任意磁盘分区，但需与支持组件位于同一磁盘分区。

-   如安装过程中提示缺少组件，请安装 [_运行库_][runtime_x64] 后再次尝试。

-   请安装 [常用软件](#常用软件) 。

<!-- 相关链接 -->

[support]: http://server.haithing.com/ois/windows/support/support.exe '支持组件'
[setup]: http://server.haithing.com/ois/windows/ '安装包'
[runtime_x86]: http://server.haithing.com/ois/windows/support/runtime_x86.exe '运行库 32 位'
[runtime_x64]: http://server.haithing.com/ois/windows/support/runtime_x64.exe '运行库 64 位'

## 系统配置与操作

### 系统配置

<div style="display: block; box-sizing: border-box; width: 80px; height: 80px; margin: .2em; padding: 0; border: none; border-radius: 30%; font-size: 2rem; line-height: 80px; text-align: center; color: #265; stroke: currentColor; background: #65e4a5 linear-gradient(135deg, #65e4a5, #44af78); fill: none; box-shadow: .1rem .1rem .2rem black; cursor: pointer;">
<svg xmlns="http://www.w3.org/2000/svg" width="100%" height="100%" viewBox="-15 -15 110 110">
    <path d="M10 50H70v5q0 5-5 5H15q-5 0-5-5V15q0-5 5-5H65q5 0 5 5V50M20 70H40V60M60 70H40" stroke-width="4" stroke-linecap="round" stroke-linejoin="round" />
</svg>
</div>

点击界面右上角 [选项] 按钮，
在弹出菜单中点击 [系统配置] 按钮，
输入系统配置密码，
进入系统配置页面。

各配置项含义如下：

1.  系统名称

    用于配置系统名称，请根据惯例及用户需求进行配置。
    如：`XX换流站阀厅红外在线监测系统` 、 `XX换流站XX接地站在线监测系统` 。

1.  副标题

    用于配置系统类型。
    一般为 `客户端` 。

1.  _Logo_

    用于配置 logo 。
    包括 `国家电网` 、 `寒霜科技` 、 `华中光电` 等选项，请依据项目情况选择。

1.  主题

    用于配置主题。
    包括 `国网绿` 、 `天空蓝` 等选项，请依据项目情况选择。

1.  管理密码

    用于配置管理密码。
    管理密码用于系统敏感操作，此密码设置后需牢记并告知用户。

1.  默认视频窗口数

    用于配置系统默认视频窗口数，默认为设备数量的两倍。

1.  看板

    用于配置主界面及视频监测界面左上角看板。

1.  选项

    高级选项包括以下选项，勾选中表示加载其对应的功能。

    -   [x] _分屏工具栏_
            此选项决定是否显示视频播放页面下方的分屏工具栏。

    -   [x] _轨道车按钮_
            此选项决定是否显示设备控制区域的轨道车控制按钮，请视是否安装轨道车选择。

    -   [x] _调焦按钮_
            此选项决定是否显示设备控制区域的焦距调节按钮，请视设备是否支持选择。

1.  模块配置

    此功能用于选择在导航栏列出的模块。
    双击模块列表项可预览模块，拖动模块列表项可加载或隐藏模块。
    已选模块列表项右侧的图标按钮用于选择主模块。

配置完成后，点击 [保存] 按钮完成配置。
如提示提交失败，可能的失败原因如下：

-   没有更改原有的配置。在未进行任何更改的情况下点击提交将会提交失败。

### 在线升级

<div style="display: block; box-sizing: border-box; width: 80px; height: 80px; margin: .2em; padding: 0; border: none; border-radius: 30%; font-size: 2rem; line-height: 80px; text-align: center; color: #265; stroke: currentColor; background: #65e4a5 linear-gradient(135deg, #65e4a5, #44af78); fill: none; box-shadow: .1rem .1rem .2rem black; cursor: pointer;">
<svg xmlns="http://www.w3.org/2000/svg" width="100%" height="100%" viewBox="-15 -15 110 110">
    <path d="M30 60H20a16 16 0 1 1 0-32a20 20 0 1 1 40 4a14 14 1 1 1 0 28H50M40 70V30l-12 12l12-12 12 12" stroke-width="4" stroke-linecap="round" stroke-linejoin="round" />
</svg>
</div>

## 数据库配置

<img src="files/navicat.png" width="80" />

推荐采用 [Navicat](#navicat) 管理数据库。

### 设备列表 (_table_dev_list_) 配置

-   `dev_id` 一般设置为 `设备型号-设备出厂日期-设备序号`，
    如 `HS-20191001-20` 。

-   `dev_name` 一般设置为 `红外设备+设备序号` 。

-   配置 _寒霜设备_ 时，
    将 `dev_type` 字段设置为 `haithing` ，
    `dev_port` 设为 `6080` 。

-   配置 _海康设备_ 时，
    将 `dev_type` 字段设置为 `hikvision` ，
    `dev_port` 设为 `8000` 。

-   电源计划、高温告警、测温记录及温度曲线等界面中仅列出 `dev_type` 为 `haithing` 的设备。

-   `login_user` 、 `login_passwd` 根据实际情况配置。

-   `ir_url` 、 `vl_url` 为视频 _rtsp_ 地址。
    配置 `ir_url` 字段将启用播放红外视频。
    配置 `vl_url` 字段将启用播放可见光视频。
    没有对应视频时，字段须设置为空（在 Navicat 中找到对应字段，点右键，选择 `"设置为 NULL"` ）。

    常用的 _rtsp_ 地址：

    -   寒霜设备红外视频地址：
        `rtsp://{ip}:8556/h264`
    -   寒霜设备可见光视频（模拟）地址：
        `rtsp://{ip}:8557/h264`
    -   海康设备主码流地址：
        `rtsp://{ip}:554/h264/ch1/main/av_stream`
    -   海康设备子码流地址：
        `rtsp://{ip}:554/h264/ch1/sub/av_stream`

-   `channel_id` 为设备通道号。
    值从 `0` 开始递增。

-   `room_id` 为设备所处房间（阀厅）。
    具体值请查阅表 `table_room_list` 。

-   ~~`window1` 与 `window2` 两字段分别用于指定 `ir_url` 与 `vl_url` 的播放窗口。~~
    此配置在 **_v6.2.0_** 后已废弃。

-   `plc_timer` 为设备自动开关机时间配置。
    如手动设置为 `0` 将标识该设备为备用设备，
    在客户端主界面及视频界面不列出。

-   其余字段无需配置。

### 变量列表 (_table_var_list_) 配置

#### 通用部分

| 字段名称   | 字段含义 | 备注                                                   |
| ---------- | -------- | ------------------------------------------------------ |
| type_id    | 变量类型 | 查阅表 `table_var_type` 获取。                         |
| var_id     | 变量标识 | 变量唯一标识号。                                       |
| var_name   | 变量名称 | 支持上下标，如 SF<sub>6</sub> 为 `SF<sub>6</sub>` 。   |
| var_unit   | 变量单位 | 支持上下标，如 m<sup>2</sup> 为 `m<sup>2</sup>` 。     |
| var_scale  | 系数值   | `value = sample / var_scale + var_offset` 。           |
| var_offset | 偏移值   | 同上。                                                 |
| var_min    | 最小值   | 当 `value < var_min` 或 `value > var_max` 时触发告警。 |
| var_max    | 最大值   | 同上。                                                 |
| usable     | 可用状态 |                                                        |

#### 数字量输入 (_DI_) 配置

| 字段名称 | 字段含义   | 备注                           |
| -------- | ---------- | ------------------------------ |
| box_id   | 采集器编号 | 查阅表 `table_box_list` 获取。 |
| box_port | 端口号     | 一般为 `1` 到 `32` 。          |

-   界面上分别用红色和绿色标识数字量的开 (`1`) 闭 (`0`) 状态。
-   数字量输入告警配置：
    -   数字量开闭状态不等同于告警状态。
    -   如需配置数字量为开 (`1`) 时告警，配置 `var_min` 与 `var_max` 为 `0` 。
    -   如需配置数字量为闭 (`0`) 时告警，配置 `var_min` 与 `var_max` 为 `1` 。
-   如需对采样值取反，可配置 `var_scale` 为 `-1` , `var_offset` 为 `1` 。

#### 数字量输出 (_DO_) 配置

| 字段名称 | 字段含义     | 备注                           |
| -------- | ------------ | ------------------------------ |
| box_id   | 采集器编号   | 查阅表 `table_box_list` 获取。 |
| box_port | 端口号       | 一般为 `1` 到 `32` 。          |
| dev_id   | 关联设备编号 | 需关联红外设备时填写设备编号。 |

#### 模拟量输入 (_AI_) 配置

| 字段名称                 | 字段含义   | 备注                               |
| ------------------------ | ---------- | ---------------------------------- |
| box_id                   | 采集器编号 | 查阅表 `table_box_list` 获取。     |
| box_port                 | 端口号     | 一般为 `1` 到 `8` 。               |
| hall_range_begin         | 量程起始值 |                                    |
| hall_range_end           | 量程结束值 |                                    |
| hall_zero                | 零漂值     |                                    |
| box_port_reserve         | 端口号     | 装有小量程霍尔传感器时配置。下同。 |
| hall_range_begin_reserve | 量程起始值 |                                    |
| hall_range_end_reserve   | 量程结束值 |                                    |
| hall_zero_reserve        | 零漂值     |                                    |

-   如量程为 `0 - 500A` 的霍尔传感器，配置 `hall_range_begin` 为 `0` , `hall_range_end` 为 `500` 。
-   如量程为 `±200A` 的霍尔传感器，配置 `hall_range_begin` 为 `-200` , `hall_range_end` 为 `200` 。
-   反向安装霍尔传感器时，调换 `hall_range_begin` 与 `hall_range_end` 。

## 常见问题 (FAQ)

### 通用 (General)

#### :question: 有技术问题怎么办

1. 建议您在提问前，大致阅读一下操作手册，了解系统相关功能。

1. 查看本章节常见问题的解答。

1. 在 [issues](https://github.com/haithing/manual/issues) 上提问并附上详细说明。

### 界面 (User Interface)

#### :question: 怎么修改界面标题与 logo 等信息

请参阅 [系统配置](#系统配置) 。

#### :question: 主界面左上角的设备布局图和现场不一致怎么办

点击 **设备布局** 界面右下角 [编辑模式] 按钮，
输入管理密码，进入编辑模式。
在左下角弹出菜单中选择预设的布局方案。
如没有和现场一致的布局方案可手动拖动设备图标调整位置，
在设备图标上单击可调整设备角度。
改动实时生效。
编辑完成后点击 [结束编辑] 按钮退出编辑模式。

#### :question: 界面支持快捷键操作吗

界面支持的快捷键如下表：

|      按键      | 操作            |      按键      | 操作            |
| :------------: | --------------- | :------------: | --------------- |
|    **Home**    | 打开主界面      |     **0**      | 打开选项菜单    |
|     **1**      | 打开第 1 个模块 |     **2**      | 打开第 2 个模块 |
|     **3**      | 打开第 3 个模块 |     **4**      | 打开第 4 个模块 |
|     **5**      | 打开第 5 个模块 |     **6**      | 打开第 6 个模块 |
|     **7**      | 打开第 7 个模块 |     **8**      | 打开第 8 个模块 |
|   :arrow_up:   | 云台向上移动    |  :arrow_down:  | 云台向下移动    |
|  :arrow_left:  | 云台向左移动    | :arrow_right:  | 云台向右移动    |
|    **PgUp**    | 轨道车向上移动  |    **PgDn**    | 轨道车向下移动  |
|     **-**      | 可见光倍率变小  |     **+**      | 可见光倍率变大  |
|    **&lt;**    | 红外近焦调节    |    **&gt;**    | 红外远焦调节    |
| **Ctrl+Alt+F** | 红外自动聚焦    |                |                 |
| **Ctrl+Alt+S** | 视频抓图        | **Ctrl+Alt+R** | 视频录像        |
| **Ctrl+Alt+1** | 选取第 1 台设备 | **Ctrl+Alt+2** | 选取第 2 台设备 |
| **Ctrl+Alt+3** | 选取第 3 台设备 | **Ctrl+Alt+4** | 选取第 4 台设备 |
| **Ctrl+Alt+5** | 选取第 5 台设备 | **Ctrl+Alt+6** | 选取第 6 台设备 |
| **Ctrl+Alt+7** | 选取第 7 台设备 | **Ctrl+Alt+8** | 选取第 8 台设备 |

### 报表 (Report)

#### :question: 无法下载报表怎么办

> :notebook: 在 [巡航报表] 界面点击下载报表没有反应，或下载后文件名类似 `2019-10-01_xls` 且无法打开。

此为操作系统 bug ，暂无法解决。
系统重启后可恢复。

## 附录

### 常用软件

#### _Git_

> https://www.git-scm.com/download

#### _Visual Studio Code_

> https://code.visualstudio.com/download

#### _Termius_

> https://www.termius.com/download

**_以下软件仅支持在公司内网下载。_**

#### _Xshell_

> http://server.haithing.com/ois/windows/support/xshell.exe

#### _Navicat_

> http://server.haithing.com/ois/windows/support/navicat.zip

#### _WinRAR_

> http://server.haithing.com/ois/windows/support/winrar.exe
