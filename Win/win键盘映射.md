# Win 修改键盘映射
## 1. 参考教程
[1](https://blog.zhpjy.com/archives/12.html#:~:text=%E5%B0%86%20wasd%20hjkl%20%E6%98%A0%E5%B0%84%E6%88%90%E6%96%B9%E5%90%91%E9%94%AE%201%20%E7%A1%AC%E4%BB%B6%E8%A7%A3%E5%86%B3%20%E9%94%AE%E4%BD%8D%E8%B0%83%E6%95%B4%E5%8E%9F%E7%90%86%E4%B8%8A%E5%B0%B1%E6%98%AF%E8%A6%81%E5%AF%B9%E8%BE%93%E5%85%A5%E7%9A%84%E6%8C%89%E9%94%AE%E4%BF%A1%E5%8F%B7%E5%81%9A%E4%B8%80%E6%AC%A1%E8%BD%AC%E6%8D%A2%E7%BD%A2%E4%BA%86%E3%80%82%20%E4%BA%8E%E6%98%AF%E6%9C%89%E5%A4%A7%E4%BD%AC%E5%81%9A%E4%BA%86%E4%B8%AA%E4%B8%9C%E8%A5%BF%E5%8F%AB%E5%81%9A,I%20%E7%BF%BB%E9%A1%B5%E3%80%82%20%E6%9C%80%E5%90%8E%E7%94%9F%E6%88%90%E4%BA%86%20exe%20%E8%AE%BE%E7%BD%AE%E4%B8%BA%E5%BC%80%E6%9C%BA%E5%90%AF%E5%8A%A8%E3%80%82%20%E4%B8%8B%E8%BD%BD%EF%BC%9A%20wasd_hkjl_ui.zip%20)

[2](https://stackoverflow.com/questions/10334603/what-does-an-asterisk-mean-at-the-beginning-of-an-ahk-scripts-line)

[3](https://www.autoahk.com/archives/39828)

## 2. 安装autohotkey

## 3. 编辑map.ahk

我的依然保持ubuntu下的快捷键设置

$$
Shift+Caps\rightarrow Esc
\\
Caps+h\rightarrow Left
\\
Caps+l\rightarrow Right
\\
Caps+k\rightarrow Up
\\
Caps+j\rightarrow Down
\\
Caps+i\rightarrow Home
\\
Caps+o\rightarrow End
$$

```c
;关闭caps功能
SetCapsLockState, AlwaysOff

;左win+apsLock为caps
LWin & CapsLock::CapsLock

;设置caps+hjkl为方向键
CapsLock & h::
if GetKeyState("Shift", "D")
    if GetKeyState("Alt", "D")
        Send +!{Left}
    else if GetKeyState("Ctrl", "D")
        Send +^{Left}
    else
        Send +{Left}
else if GetKeyState("Ctrl", "D")
    if (GetKeyState("Alt", "D"))
        Send !^{Left}
    else
        Send ^{Left}
else if GetKeyState("Alt", "D")
    Send !{Left}
else
    Send {Left}
return

CapsLock & j::
if GetKeyState("Shift", "D")
    if GetKeyState("Alt", "D")
        Send +!{Down}
    else if GetKeyState("Ctrl", "D")
        Send +^{Down}
    else
        Send +{Down}
else if GetKeyState("Ctrl", "D")
    if (GetKeyState("Alt", "D"))
        Send !^{Down}
    else
        Send ^{Down}
else if GetKeyState("Alt", "D")
    Send !{Down}
else
    Send {Down}
return

CapsLock & k::
if GetKeyState("Shift", "D")
    if GetKeyState("Alt", "D")
        Send +!{Up}
    else if GetKeyState("Ctrl", "D")
        Send +^{Up}
    else
        Send +{Up}
else if GetKeyState("Ctrl", "D")
    if (GetKeyState("Alt", "D"))
        Send !^{Up}
    else
        Send ^{Up}
else if GetKeyState("Alt", "D")
    Send !{Up}
else
    Send {Up}
return

CapsLock & l::
if GetKeyState("Shift", "D")
    if GetKeyState("Alt", "D")
        Send +!{Right}
    else if GetKeyState("Ctrl", "D")
        Send +^{Right}
    else
        Send +{Right}
else if GetKeyState("Ctrl", "D")
    if (GetKeyState("Alt", "D"))
        Send !^{Right}
    else
        Send ^{Right}
else if GetKeyState("Alt", "D")
    Send !{Right}
else
    Send {Right}
return


;caps+i 向上翻页 
CapsLock & i:: send, {Home}
;caps+u 向下翻页
CapsLock & o:: send, {End}

+CapsLock::Escape

return

```
## 4. 编译map.ahk生成map.exe

右键`ahk`文件选择GUI编译

在打开的GUI里面选择source为`ahk`文件

destination默认

basefile选择`Ahk2Exe.exe`

## 5. 开机运行设定


```sh
C:\Users\AnotherTT\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup
# exe文件放到这里即可
```
