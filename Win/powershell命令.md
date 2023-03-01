## 教程

https://www.yiibai.com/powershell/powershell-functions.html

## 我的函数

```shell
oh-my-posh init pwsh --config $env:POSH_THEMES_PATH\atomic.omp.json | Invoke-Expression 
#Import-Module 'C:\tools\poshgit\dahlbyk-posh-git-9bda399\src\posh-git.psd1'

#add vim path
$SCRIPTPATH = "C:\Program Files (x86)\Vim"
$VIMPATH = $SCRIPTPATH + "\vim90\vim.exe"
 
#set alias vi/vim
Set-Alias vi $VIMPATH
Set-Alias vim $VIMPATH

#web-search
function google($que) {start www.google.com/search?q=$que}

function bing($que) {start www.bing.com/search?q=$que}


#easy commands linux
function open() {ii .}
function q() {exit}
function touch($filename) {new-item $filename}

#easy git
function gitee() {
    cd ~/gitee
    ii .
}

function gitall($msg) {
    cd ~/gitee
    git add .
    git commit -m $msg
    git push
}
```

