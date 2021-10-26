---
title: Vimrc
description: A customized vimrc file
published: true
date: 2021-10-09T16:20:24.681Z
tags: rc, vim
editor: markdown
dateCreated: 2021-10-09T16:20:03.366Z
---

```plaintext
set tabstop=4
set shiftwidth=4
set expandtab
syntax on
set t_Co=256
"colorscheme codedark"
"set t_ut=
set enc=utf-8
set guifont=Powerline_Consolas:h11

"set foldmethod=indent
"set foldnestmax=3
"set nofoldenable

set wrap
set encoding=utf-8
"set display+=lastline

set noswapfile
"set laststatus=2
"set ruler
"set wildmenu
"set cursorline

:map <F2> :!ls<CR>:e
:nnoremap <C-I><C-I><C-I> <C-W><C-W>
:nnoremap <C-I><C-I> <C-t>
:nnoremap <C-I> <C-]>
:set tabstop=4
:set softtabstop=4
:set number relativenumber
:set showcmd
:set wildmenu
:set lazyredraw
:set showmatch
:set incsearch
:set hlsearch
:set shiftwidth=4
:set expandtab
:colorscheme desert
:syntax enable
:nnoremap <leader><space> :nohlsearch<CR>

highlight Normal term=none cterm=none ctermfg=White ctermbg=Black gui=none guifg=White guibg=Black
highlight DiffAdd cterm=none ctermfg=bg ctermbg=Green gui=none guifg=bg guibg=Green
highlight DiffDelete cterm=none ctermfg=bg ctermbg=Red gui=none guifg=bg guibg=Red
highlight DiffChange cterm=none ctermfg=bg ctermbg=Yellow gui=none guifg=bg guibg=Yellow
highlight DiffText cterm=none ctermfg=bg ctermbg=Magenta gui=none guifg=bg guibg=Magenta
```