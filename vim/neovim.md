# nvim配置教程

## Ref.
https://www.bilibili.com/video/BV1QL4y147VD/?spm_id_from=333.337.search-card.all.click&vd_source=9fc1aeab20d64d4315c451b9c18d30d8
https://www.bilibili.com/video/BV14a41147ap/?spm_id_from=333.337.search-card.all.click&vd_source=9fc1aeab20d64d4315c451b9c18d30d8

[**repo**:](https://github.com/LunarVim/Neovim-from-scratch)

在命令中输入Lexplore(可以tap)
就可以打开一个类似于renger的文件管理窗口

再次输入可以关闭

上下左右可以切换命令记录

中文自动高亮有点烦

首先来修一下拼写检查的高亮问题

其次不建议多搞很多配置，这边给一个教程

找到报错问题了，是在init文件的最后一个auto command中

可能是这个插件使得拼写检查变严格了

https://www.bilibili.com/video/BV1Td4y1578E/?spm_id_from=333.337.search-card.all.click&vd_source=9fc1aeab20d64d4315c451b9c18d30d8

根据这个教程，安装了lunarvim

lunarvim在官网上就可以找的到，可以一键下载。

有一个问题，就是lunarvim自动会对各种语言进行拼写检查（包括neovim），就会显示一大堆红色高亮或波浪线，很耀眼。

可以在vim命令行输入`:set nospell`来实现避免拼写，
也可以把这一行加入到 config中
```lua
vim.opt.spell = false
-- 但是不管用，很奇怪
-- 解决方案是：
vim.opt.spelllang = zh
-- 更改拼写语法
```

## colorscheme

其实theme指的就是colorscheme

直接在config.lua中加

找到lvim.plugins

加github地址即可

如果没有自动更新，运行`:PackerSync`

下载的插件在：
`/home/raccoon/.local/share/lunarvim/site/pack/packer/start`

## lunar交流群代办

## lunar clipboard

报错找不到粘贴支持

参考这个文章下载xclip
https://blog.csdn.net/lxyoucan/article/details/124326933

## lunar spelllang 找不到词典

首先声明，在spelllang中设置zh的方式是不对的。因为vim/spell中没有这个词典，默认拼写是en加cjk
https://zhuanlan.zhihu.com/p/24986495
参考这个链接

至于为什么设置了false还是会有拼写检查，这个我得去lunar中文用户群体里面问问

至于解决方案嘛，设置为cjk就好了，注意加引号
