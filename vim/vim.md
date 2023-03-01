# Vim
## 1. 插入
```sh
i光标前插入
a光标后插入
shift a 行尾插入
shift i 行首插入
```
## 2. 移动

```sh
hjkl左下上右
w下一个单词开头
b上一个单词开头/本单词开头
e下一个单词结尾/本单词结尾
ge上一个单词结尾
0行首
^第行首第一个非空字符
$行尾
gg第一行
G最后一行
f{char}下一个char位置
F{char}上一个char位置
t{char}下一个char前一个字
T{char}上一个char后一个字
;重复上次的查找命令
,反向查找上次的命令
```
## 3. 修改

```sh
d删除
c修改
u撤销
y复制
p粘贴
```

## 4. 切换
```sh
gd进入定义
ctrl O返回
gh显示函数标签
gt往后跳标签
gT往前跳标签
num gt调到数字对应的标签页
ctrl 0调到侧边栏
	然后jk上下
	空格展开文件夹
	空格打开文件
	l打开文件并进入文件
	回车也行
分屏操作
	ctrl num跳到分屏
```

## 5. vscode

临时禁用vim

toogle vim mode命令
