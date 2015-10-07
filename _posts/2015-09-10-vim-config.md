---
layout: post
title: vim配置
tags: vim
categories: 
  - program
  - tools
---

一份适合于自己的`vim`配置总能帮助我们提升工作效率,下面分享一份我目前的vim配置!!!

<!--more-->
### config list
---
```vim
"Configuration file for vim
set modelines=0		"CVE-2007-2438

"Normally we use vim-extensions. If you want true vi-compatibility
"remove change the following statements
set nocompatible	"Use Vim defaults instead of 100% vi compatibility
set backspace=2		"more powerful backspacing

"Don't write backup file if vim is being called by "crontab -e"
au BufWrite /private/tmp/crontab.* set nowritebackup nobackup
"Don't write backup file if vim is being called by "chpass"
au BufWrite /private/etc/pw.* set nowritebackup nobackup
"语法高亮
syntax enable
syntax on
set nu!
set history=1000	"记录历史行
set autoindent		"vim使用自动对起，也就是把当前行的对起格式应用到下一行；
set smartindent		"依据上面的对起格式，智能的选择对起方式，对于类似C语言编写上很有用
"第一行设置tab键为4个空格，第二行设置当行之间交错时使用4个空格
set tabstop=4
set shiftwidth=4
set showmatch		"设置匹配模式，类似当输入一个左括号时会匹配相应的那个右括号
set guioptions-=T	"去除vim的GUI版本中的toolbar
set vb t_vb=		"当vim进行编辑时，如果命令错误，会发出一个响声，该设置去掉响声
set ruler			"在编辑过程中，在右下角显示光标位置的状态行
set incsearch		"查找内容时根据输入快速匹配
set laststatus=2    "启动显示状态行(1),总是显示状态行(2)
set autoread		"设置当文件被改动时自动载入
set showmatch		"显示括号配对
set wrap			"自动换行
set hlsearch		"高亮search命中的文本

set foldenable		" 代码折叠  
	" 折叠方法  
	" manual    手工折叠  
	" indent    使用缩进表示折叠  
	" expr      使用表达式定义折叠  
	" syntax    使用语法定义折叠  
	" diff      对没有更改的文本进行折叠  
	" marker    使用标记进行折叠, 默认标记是 {{{ 和 }}}  
set foldmethod=indent 
"查看折叠代码别名
nmap <silent> ee zR	
"set foldcolumn=4	" 在左侧显示折叠的层次  
set cursorline		" 突出显示当前行

set t_Co=256
"colorscheme desert	"经典配色
"colorscheme koehler
colorscheme monokai	"sublime配色

set paste		"设置粘贴模式，这样粘贴过来的程序代码就不会错位 
set enc=utf-8
set fileencodings=utf-8,gbk,ucs-bom,cp936,latin1,big5,utf-16
set encoding=utf-8
set fileencoding=utf-8
set termencoding=utf-8


"""""""""""
"NERDTree "
"""""""""""
map nd :NERDTree
map nc :NERDTreeClose


""""""""""""""""
"window manager"
""""""""""""""""
map <tab> <c-w><c-w>
nmap <silent> ( 5<c-w><
nmap <silent> ) 5<c-w>>
nmap <silent> - 10<c-w>-
nmap <silent> = 10<c-w>+


"新建.sh文件，自动插入文件头 
autocmd BufNewFile *.sh exec ":call SetTitle()"
autocmd BufNewFile * normal G
"autocmd BufNewFile * normal o 
"定义函数SetTitle，自动插入文件头 
func SetTitle() 
	"如果文件类型为.sh文件 
	if &filetype == 'sh' 
		call setline(1,"\#########################################################################") 
		call append(line("."), "\# File Name: ".expand("%")) 
		call append(line(".")+1, "\# Copyright (c) HUSTLH, Inc. All Rights Reserved") 
		call append(line(".")+2, "\# Email: mrvincentfirst_lh@163.com") 
		call append(line(".")+3, "\# Created Time: ".strftime("%F %T")) 
		call append(line(".")+4, "\# Last Modified: ".strftime("%F %T"))
		call append(line(".")+5, "\#########################################################################") 
		call append(line(".")+6, "\#!/bin/bash") 
		call append(line(".")+7, "") 
	endif
endfunc

"修改.sh文件，插入最近更改时间
"autocmd BufWrite,BufWritePre,FileWritePre  *.sh exec ":call LastModified()"  
autocmd BufWrite,BufWritePre,FileWritePre  *.sh   ks|call LastModified()|'s  
func LastModified()
	exe "1,$ s/Last Modified: .*/Last Modified: " .
			\ strftime("%F %T") . "/e"
endfunc
```

### 配色方案下载
---
* [monokai配色下载(sublime配色)](https://github.com/crusoexia/vim-monokai.git)

### 相关插件下载
---
* `NERDTree:`[vim官方下载](http://www.vim.org/scripts/script.php?script_id=1658)或[github下载](https://github.com/scrooloose/nerdtree.git)
