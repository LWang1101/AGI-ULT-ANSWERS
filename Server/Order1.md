文件

打开文件夹 cd xxx

返回上一级 cd..

返回根目录 cd

查看文件下内容 ls

创建目录 mkdir 名称

复制文件 cp [file] [path]

删除文件夹 rm -rf [folder] (其中-r表示递归删除)


命令输入快捷键

ctrl + w —往回删除一个单词，光标放在最末尾  

ctrl + u 删除光标以前的字符 

ctrl + k 删除光标以后的字符 

ctrl + a 移动光标至字符头 

ctrl + e 移动光标至字符尾 

ctrl + l 清屏

Tab 自动补全

shift + insert 粘贴

鼠标左键选中，然后右键复制(因为ctrl+c这里是keyboard interrupt键盘中断)

鼠标中键粘贴

硬件

任务管理器 top，htop

  只看某个进程 top -p PID
  
  只看某个用户的进程 top -u USER_name    

查看显卡状态 nvidia-smi

查看CPU  lscpu

查看内存 free -h  #-h表示16进制

查看硬盘 df -lh 

查看硬盘总体情况 lsblk

查看CUDA版本 cat /usr/local/cuda/version.txt

查看cudnn版本 cat /usr/local/cuda/include/cudnn.h | grep CUDNN_MAJOR -A 2 

压缩

tar(选项)(参数)

-c压缩

-x解压

-v显示

-f指定文件名

-z涉及gz ，以gzip 

解压的例子：tar -zxvf dataset.tar.gz

shell

bash [options] [file]

例子 bash config.sh

后台

--用screen或者tmux或者其他的都行。

创建窗口 screen -S 名称 

显示现有窗口 screen -ls

恢复窗口 screen -r 名称

强制删除 screen -S 名 -X quit

强制恢复 screen -D  -r 名称  (进入Attached)

在窗口下：离开窗口 ctrl+a，d

在窗口下：删除窗口 ctrl+a，k

python

运行程序 python xxx.py

进入python脚本 python

查看python版本 python --version

安装命令

建立设置，prefix表示安装路径 ，示例：

./congfigure --prefix=/xxx/xxx/

编译并安装

make -j8 && make install

make是编译，-j8表示8个线程，&&连接第二个命令，make install安装

有时候会用到的

查看被系统Killed日志  sudo egrep -i -r 'killed process' /var/log

输出重定向

大量print信息不适合在窗口显示的情况。

在命令后方输入>文件名 2>&1

例如 python xxx.py >log 2>&1

2为标准错误，&1为标准输出。命令意为标出顺出定向到log文件，标准错误定向到标准输出也定向到log文件

高级screen

选项

-A 　将所有的视窗都调整为目前终端机的大小。

-d <作业名称> 　将指定的screen作业离线。

-h <行数> 　指定视窗的缓冲区行数。

-m 　即使目前已在作业中的screen作业，仍强制建立新的screen作业。

-r <作业名称> 　恢复离线的screen作业。

-R 　先试图恢复离线的作业。若找不到离线的作业，即建立新的screen作业。

-s 　指定建立新视窗时，所要执行的shell。

-S <作业名称> 　指定screen作业的名称。

-v 　显示版本信息。

-x 　恢复之前离线的screen作业。

-ls或--list 　显示目前所有的screen作业。

-wipe 　检查目前所有的screen作业，并删除已经无法使用的screen作业。

常用screen参数

screen -S yourname -> 新建一个叫yourname的session

screen -ls -> 列出当前所有的session

screen -r yourname -> 回到yourname这个session

screen -d yourname -> 远程detach某个session

screen -d -r yourname -> 结束当前session并回到yourname这个session

screen -X -S [session # you want to kill] quit

在每个screen session 下，所有命令都以 ctrl+a(C-a) 开始。

C-a ? -> 显示所有键绑定信息

C-a c -> 创建一个新的运行shell的窗口并切换到该窗口

C-a n -> Next，切换到下一个 window 

C-a p -> Previous，切换到前一个 window 

C-a 0..9 -> 切换到第 0..9 个 window

Ctrl+a [Space] -> 由视窗0循序切换到视窗9

C-a C-a -> 在两个最近使用的 window 间切换 

C-a x -> 锁住当前的 window，需用用户密码解锁

C-a d -> detach，暂时离开当前session，将目前的 screen session (可能含有多个 windows) 丢到后台执行，并会回到还没进 screen 时的状态，此时在 screen session 里，每个 window 内运行的 process (无论是前台/后台)都在继续执行，即使 logout 也不影响。 

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
