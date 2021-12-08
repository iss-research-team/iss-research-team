# iSS数控中心服务器使用手册

由于中心服务器安装linux系统,使用方式有较大的变化,这里对服务器连接流程做一说明。

## 1. 连接数控中心内网,登录堡垒机,进入服务器

名称：NERC-INTERNAL

密码：nerc@123

注意:在内网只能连接内部服务器,无法访问外部资源

在浏览器中输入: https://192.168.69.150/ 显示如下:

![image-20211208094015672](C:\Users\15842\Desktop\iSS数控中心服务器使用手册\iSS数控中心服务器使用手册1.1.assets\image-20211208094015672-16389276214981.png)

登录堡垒机: 

用户名：liuyuhan 

密码：Logan125689 

显示如下: 

![image-20211208093608234](C:\Users\15842\Desktop\iSS数控中心服务器使用手册\iSS数控中心服务器使用手册1.1.assets\image-20211208093608234.png)

点击SSH,选择web,进入服务器。

## 2. 服务器主要环境说明

> ubuntu==20.04
>python3==3.8.10
> nvidia_driver==465.19.01
>cuda==11.3
> cudnn==8.2.1
>torch==1.10.0
> transformers==4.12.3



## 3. 程序运行

第一次使用请在`~/`（`/home/iss/`）目录下创建一个个人文件夹。

程序可上传至github，在服务器端通过`git clone`进行代码下载至个人文件夹。

当有大文件（>15m）需要拷贝时，请联系刘宇涵或刘铭。

注意：服务器目前可以使用screen供多人运行，具体使用方法见下。

## 4.screen

**Screen**是一款用于命令行终端切换的自由软件。用户可以通过该软件同时连接多个本地或远程的命令行会话，并在其间自由切换，即使网络连接中断，用户也不会失去对已经打开的命令行会话的控制。

### 常用的screen命令

```shell
screen -S session_name -> 新建一个叫session_name的session
screen -ls -> 列出当前所有的session
screen -r session_name -> 回到session_name这个session
screen -d session_name -> 远程detach某个session
screen -d -r session_name -> 结束当前session并回到yourname这个session
screen -S session_name -X quit -删除session
```

### 使用方法

⭐进入服务器后，我们可以使用`screen -S yourname`创建一个叫做`yourname`的会话，之后需要使用`screen -r yourname`进入到该会话中，进行后续的操作，如运行实验程序。使用`Ctrl + a +d`命令可以暂时离开该会话，将该会话丢到后台进行处理，之后可以使用`screen -r yourname`返回该会话。

在screen 会话下，所有命令都以`Ctrl + a`开始，如命令`Ctrl + a + d`，用于离开当前会话。

每个会话中又可以使用`screen -S`建立多个window。在不同的window之间可以用`Ctrl + a + n/p`等命令来切换。

### screen session中的命令

```shell
# C-a代表Ctrl+a
C-a ? -> 显示所有键绑定信息
C-a d -> detach，暂时离开当前session，将目前的 screen session (可能含有多个 windows) 丢到后台执行，并会回到还没进 screen 时的状态，此时在 screen session 里，每个 window 内运行的 process (无论是前台/后台)都在继续执行，即使 logout 也不影响。 
C-a c -> 创建一个新的运行shell的窗口并切换到该窗口
C-a n -> Next，切换到下一个 window 
C-a p -> Previous，切换到前一个 window 
C-a 0..9 -> 切换到第 0..9 个 window
C-a [Space] -> 由视窗0循序切换到视窗9
C-a C-a -> 在两个最近使用的 window 间切换 
C-a x -> 锁住当前的 window，需用用户密码解锁
C-a z -> 把当前session放到后台执行，用 shell 的 fg 命令则可回去。
C-a w -> 显示所有窗口列表
C-a t -> time，显示当前时间，和系统的 load 
C-a k -> kill window，强行关闭当前的 window
C-a [ -> 进入 copy mode，在 copy mode 下可以回滚、搜索、复制就像用使用 vi 一样
    C-b Backward，PageUp 
    C-f Forward，PageDown 
    H(大写) High，将光标移至左上角 
    L Low，将光标移至左下角 
    0 移到行首 
    $ 行末 
    w forward one word，以字为单位往前移 
    b backward one word，以字为单位往后移 
    Space 第一次按为标记区起点，第二次按为终点 
    Esc 结束 copy mode 
C-a ] -> paste，把刚刚在 copy mode 选定的内容贴上
```





