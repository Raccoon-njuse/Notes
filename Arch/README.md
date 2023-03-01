# ArchLinux

![image-20230223082638948](/home/raccoon/.config/Typora/typora-user-images/image-20230223082638948.png)

## 前言

正如我预料到的那样，选择arch确实是一个正确的决定，在高度定制的环境和详细的说明文档中，亲自搭建自己的工作区，是一种莫大的乐趣，这种乐趣本身也是一种学习。

在使用arch的过程中往往会遇到很多发疯的时刻，比方说明明按照教程来但是却完全不符合我的预期，这种情况我戏称为**“计算机学科不存在了”**。这种发疯常常让人达到废寝忘食的程度，可能早晨9点起来一直趴在桌子上到下午四点，为了一个bug，甚至可以一直不吃饭。亦或许会放弃考试复习的时间。兴许是有些不务正业，但在软院大三的高压学习和摆烂氛围下找到一件感兴趣的事情也许并不算一件坏事。至少，我已经很少感受到这种兴奋和探索的乐趣了。

正如我和哲源所说，解决arch的问题，应当抱有一种**“技术爆炸”**的态度，只有学习的东西足以覆盖出现bug的问题域，才能有较大的把握解决它。而当你没有完全掌握这个领域的知识却要使用它时，就要做好你无法掌控的准备。这就好比火鸡和农场主，我在农场主的帮助下，可以接触到计算机不存在了的原因，其实是更深层的计算机知识，因此，只有我认知范围内的计算机学科可能不存在，更大范围内的依然是真理。

感谢所有在我使用archlinux中提供帮助的教程、博客和亲授操作的朋友们。

2023.2.23

## 一些基本概念

- diaplay manager：显示管理器，也是arch login的ui。 我使用了lightdm 来代替KDE桌面的管理器
- i3 windows manager：窗口管理器，脱离了桌面环境的管理方式，轻量级，高效化。但需要自己配置很多东西
- DE（desktop environment）：桌面环境，传统的桌面管理方式，将桌面显示为任务栏和堆叠化窗口
- yay：arch下的包管理器

## 1. ArchLinux安装

- lightdm自动登陆：

```sh
sudo vi /etc/lightdm/lightdm.conf

#change follow,在以下标记中寻找即可
[Seat:*]
autologin-user=raccoon
autologin-user-timeout=0
```



## 2. i3wm安装配置

```sh
sudo pacman -S i3
kate ~/.config/i3/config &
```

i3的配置文件在~/.config/i3/config中，今后将以该文件和~/.zshrc来管理大部分的操作



### 2.1 显示管理

reference：[1](https://blog.csdn.net/syh_486_007/article/details/71158022) [2](https://www.cnblogs.com/WaterGe/p/12133555.html) [3](https://zhuanlan.zhihu.com/p/71536834)

通过xrandr即可

```sh

xrandr #查看设备
xrandr --output DP-1 --auto --output eDP-1 --off #关闭其中一个设备
xrandr --output eDP-1 --auto --output DP-1 --off #之在笔记本上显示
xrandr --output DP-1 --auto --above eDP-1 --auto #多屏协动
千万不要尝试把两个屏幕都关掉!!!
参考3中有多屏移动工作区的命令，我认为不常用
```

将这几行命令写入zshrc

```sh
#显示屏
function disp() {
    if [[ $1 == 'aoc' ]];then
        xrandr --output DP-1 --auto --output eDP-1 --off
        return
    fi
    if [[ $1 == 'bjb' ]];then
        xrandr --output eDP-1 --auto --output DP-1 --off
        return
    fi
    if [[ $1 == 'all' ]];then
        xrandr --output DP-1 --auto --above eDP-1 --auto
        return
    fi
}
```

遇到问题就拔下来重新插

注意, 盲打的时候是否是中文输入法

其次, 可以使用arandr进行图形化的配置

### 2.2 触控板管理

references：[知乎](https://zhuanlan.zhihu.com/p/116957768) [archwiki](https://wiki.archlinux.org/title/Touchpad_Synaptics)

参照archwiki，安装xf86-input-synaptics

在/etc/X11/xorg.cinf.d/70-synaptics.conf中添加

```sh
Section "InputClass"
    Identifier "touchpad"
    Driver "libinput"
    MatchIsTouchpad "on"
    Option "Tapping" "on"
    Option "NaturalScrolling" "true"
    Option "ClickMethod" "clickfinger"
    Option "RBCornerButton" "3"
EndSection
```

### 2.3 窗口外观

参见文档

https://i3wm.org/docs/userguide.html#vim_like_marks

#### 边框:

可以通过设置pixel取消标题栏

gap_inner设置窗口之间的间隙

#### 颜色：

一个较为一致性的方案是，通过X桌面设置，详见用户手册4.18

```sh
# ~/.Xresources 应该包含这样一行
# *color0: #121212
# 并且必须正确加载，例如，通过使用
# xrdb ~/.Xresources
# 该值由其他应用程序获取（例如，URxvt 终端
# 模拟器）并且可以像这样在 i3 中使用：
set_from_resource $black i3wm.color0 #000000
```

更为细致的配色方案：在i3config中 详见4.22

```sh
经过多伦尝试，我发现对应的颜色显示地点如下：
focused：border是多窗口并列时候的标签边框，back是标签背景，text是文字，ind好像是右边框？，child是子边框，也就是默认边框
inactive：指的是容器顶部非聚焦
unfocus：非容器顶部非聚焦
# class                 border  backgr. text    indicator child_border
#聚焦的窗口  红 浅蓝 淡绿 橙色 粉红
client.focused          #FF0000 #87CEFA #90EE90 #FF8C00   #FFB6C1
client.focused_inactive #333333 #5f676a #ffffff #484e50   #808080
client.unfocused        #333333 #222222 #888888 #292d2e   #808080
client.urgent           #2f343a #900000 #ffffff #900000   #900000
client.placeholder      #000000 #0c0c0c #ffffff #000000   #0c0c0c
client.background       #f1948a
目测87CEFA和 8FBC8F 一个蓝色一个绿色 配起来都不错
语法：
<colorclass> <border> <background> <text> <indicator> <child_border>
其中 colorclass 可以是以下之一：
client.focused 
当前具有焦点的客户。
client.focused_inactive
一个客户端，它是其容器的焦点之一，但目前没有焦点。
client.focused_tab_title
作为获得焦点的容器的父项但未直接获得焦点的选项卡或堆栈容器标题。如果未指定，则默认为 focused_inactive，并且不使用指示器和 child_border 颜色。
client.unfocused
不是其容器的焦点之一的客户端。
client.urgent 
已激活紧急提示的客户端。
client.placeholder
背景和文本颜色用于绘制占位符窗口内容（恢复布局时）。边框和指示器被忽略。
client.background
背景颜色将用于绘制客户端窗口的背景，客户端将在其上呈现。只有未覆盖此窗口整个区域的客户端才会显示颜色。请注意，此颜色类仅采用一种颜色。

请注意，对于窗口装饰，子窗口周围的颜色是“child_border”，而“border”颜色只是标题栏周围的两条细线。
指示器颜色用于指示将在何处打开新窗口。对于水平拆分容器，右边框将涂上指示器颜色，对于垂直拆分容器，底部边框。这仅适用于拆分容器内的单个窗口，否则无法将其与拆分容器外的单个窗口区分开来。
```

蓝粉配色：

```sh
# class                 border  backgr. text    indicator child_border
client.focused          #FFB6C1 #FFB6C1 #ffffff #000000   #FFB6C1
client.focused_inactive #FFB6C1 #87CEFA #ffffff #484e50   #87CEFA
client.unfocused        #FFB6C1 #87CEFA #ffffff #484e50   #87CEFA
client.urgent           #2f343a #900000 #ffffff #900000   #900000
client.placeholder      #000000 #0c0c0c #ffffff #000000   #0c0c0c

client.background       #f1948a
```





### 2.4 设置固定工作区:

通过xprop获取窗口类型

然后就可以将某个类型应用的默认打开方式设置到某个工作区啦

```sh
assign [class="firefox"] 2
```

### 2.5 选定浮动窗口

一个很有意思的现象是，我在设置
```sh
for_window [class="alactritty"] floating enable
```
的时候，发现设置无效，解决方案改成大写
我猜这里的是desktop文件里的识别名称，而exec里面放的就是终端命令

窗口管理之--默认初始大小，透明化

### 2.6 设定窗口默认布局

使用i3-layout进行管理：

https://github.com/eliep/i3-layouts#layouts

需要进行：i3l启动，工作区布局绑定，方向移动绑定

坏处是容器可能变乱，vstack布局暂时没啥问题

### 2.7 rofi

- install

```shell
sudo pacman -S rofi
```

- themes

https://github.com/newmanls/rofi-themes-collection#windows-11

将需要的主题文件复制到.local/share/rofi/icons即可，然后在config里面选择

配置主题应当在主题文件中，而不是在config中，rofi的config只用来设置modify和主题

- 字体

参见polybar，也是在主题文件中设置

### 2.8 polybar

- themes

https://github.com/adi1090x/polybar-themes

- 还有一些其他dotfile里面的polybar配置，可以试试

### 2.9 alacritty

- themes

https://github.com/alacritty/alacritty-theme/

关于alacritty的下载，建议去archwiki

[there](https://wiki.archlinuxcn.org/wiki/Alacritty)

经过测试，很难找到非常适合我的一款可爱粉嫩风终端配色，因此只好走赛博朋克风了

Nord还是yyds的，其他的emmm,还有第一个afterglow, dark_pastels, everforest_dark
moonlight_ii_vscode, rainbow，rose-pine， tokyo-night-storm等等

妈的。真的很难找，有时间自己做一个，我记得b站那位有教程

字体上，选择JetBrainsMono Nerd Font
至于如何更换字体，在wiki上有
logo-ls失效

### 2.10 flameshot

有卡顿，待解决

存档到文件打开卡顿，存档到粘贴板粘贴卡顿，大佬教我用

### 2.11 picom

https://wiki.archlinux.org/title/Picom

需要禁用rofi阴影，否则太怪了

透明度选项：可以调节聚焦和非聚焦透明度，可以设置opacity-rule单独为某个窗口设置透明

alacritty和rofi为80

打字窗口（popup_menu)在wintype里面设置为0.8

dock栏设置为0.75

关于圆角和模糊，暂时不准备搞了，有点卡-

更新：picom有很多版本，我选择了其中的一种：

https://www.bilibili.com/video/BV15V4y1g7L6/?spm_id_from=333.337.search-card.all.click&vd_source=9fc1aeab20d64d4315c451b9c18d30d8

这个视频链接底下有github仓库，我直接用了里面的配置，修改了一些属性，比如把聚焦和非聚焦的透明度改成一致……

但是卡顿现象还是有的，今天在4k屏上显示成功了，但是呢，很卡

### 2.12 feh

切换壁纸，加random可以随机切换

### 2.13 无道词典

终端查词的有道版本，github直接搜

## 3. 我与代理那些事

### 3.1 如何同步时间：

```sh
❯ timedatectl                                                                             ─╯
               Local time: 四 2023-02-23 10:04:17 CST
           Universal time: 四 2023-02-23 02:04:17 UTC
                 RTC time: 四 2023-02-23 02:04:18
                Time zone: Asia/Shanghai (CST, +0800)
System clock synchronized: no
              NTP service: inactive
          RTC in local TZ: no
```

no表示没有同步好时间

```sh
❯ systemctl restart systemd-timesyncd.service                                             ─╯
==== AUTHENTICATING FOR org.freedesktop.systemd1.manage-units ====
重新启动“systemd-timesyncd.service”需要认证。Authenticating as: raccoon
Password: 
==== AUTHENTICATION COMPLETE ====
```

重启服务即可

好像不是完全可以解决问题

万能的CSDN如是说:timedatectl set-local-rtc 1

### 3.2 v2raya

telegram的老哥教教用法：

```sh
#首先要看/var/log/v2raya下面的log
然后执行命令
journalctl -fu v2raya -n 100 #查看执行记录
```

<img src="/home/raccoon/Pictures/6394C08FB4BAB6DA011FBA235B4B63CE.png" width=70%>

以上报错信息的解决方案是：

大哥说我-Syu了，让我换v2raya-git，装好之后再换

但是机房电脑跑不起来，太可恶了

是否可能是没有安装v2ray内核？





## BUG

qq和i3老会闪退，有点烦，待会试试第三方qq

机房的x桌面没装好，相互关联的信息有待学习

#### 关于显示器. 
目前显示器在我已知范围内有如下bug和现象

第一是, 在xrandr显示信息时, 有时显示60+30HZ, 有时显示29HZ

显示29HZ的时候, 大概率是接口有问题, 因为windows也是这样

在显示配置中,我启用了disp脚本,用xrandr

disp all 和 aoc时,会导致两边黑屏,黑暗中摸索命令大多是没有执行的

一方面可能是输入法中文

另一方面从查阅bash记录来讲, 很有可能是没有敲进去,那怎么回事呢?我明明是新建了工作区的

ssh能否给我答案

还有时候,disp aoc没反应,或者xrandr检测不到

开机如果已经启动了显示器, 会桌面渲染卡顿(因为键盘敲reboot是可以响应的)

检测不到显示器的arandr图形化报错:
```sh
XRandR失败:
XRandR returned error code 1: b'xrandr:cannot find mode None\n
```
最新结论:
xlayoutdisplay是可以进行3840 60hz的
只是dpi有问题

 

