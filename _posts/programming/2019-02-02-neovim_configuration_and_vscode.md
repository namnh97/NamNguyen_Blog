---
title: "Neovim Configuration And VScode"
categories: [Programming, Tools]
excerpt: "Configure C++."
---

# VIM

1. Install NEOVIM
2. Install [VimVundle](https://github.com/VundleVim/Vundle.vim)
3. Edit file ~/.config/nvim/init.vim

```

filetype off
" set the runtime path to include Vundle and initialize
set rtp+=~/.config/nvim/bundle/Vundle.vim
call vundle#begin('~/.config/nvim/bundle')

" let Vundle manage Vundle, required
Plugin 'VundleVim/Vundle.vim'
Plugin 'tpope/vim-fugitive'
Plugin 'jiangmiao/auto-pairs'
Plugin 'scrooloose/nerdtree'
Plugin 'vim-airline/vim-airline'
" All of your Plugins must be added before the following line
call vundle#end()

filetype plugin indent on 

"Simple setting 
syntax enable
set tabstop=4
set shiftwidth=4
set smartindent
set enc=utf-8
set fenc=utf-8
set termencoding=utf-8
set number 

"Setting for auto pair
let g:AutoPairs = {"{": "}"}
let g:AutoPairsShortcutJump=''
let g:AutoPairsMoveCharacter=''
let g:AutoPairsShortcutBackInsert=''
let g:AutoPairsShortcutToggle =''
let g:AutoPairsShortcutFastWrap=''
let g:AutoPairsWildClosedPair=''
let g:AutoPairsMapBS=1
let g:AutoPairsMapCh=0
let g:AutoPairsCenterLine=0
let g:AutoPairsMapSpace=0
let g:AutoPairsMultilineClose=0
let g:AutoPairsFlyMode = 1
"let g:AutoPairsShortcutBackInsert=''

map <F8> :!g++  -std=c++11 -g  % && ./a.exe <CR>
map <F4> :w <bar> !g++  -std=c++11 -g % <CR>
autocmd BufNewFile *.cpp :0r /home/namnh97/.config/nvim/template.cpp
autocmd BufNewFile *.cpp :w!
map <C-n> :NERDTreeToggle<CR>
let g:NERDTreeDirArrows=0


"Copy to clipboard for neovim
function! ClipboardYank()
  call system('xclip -i -selection clipboard', @@)
endfunction
function! ClipboardPaste()
  let @@ = system('xclip -o -selection clipboard')
endfunction

vnoremap <silent> y y:call ClipboardYank()<cr>
vnoremap <silent> d d:call ClipboardYank()<cr>
nnoremap <silent> p :call ClipboardPaste()<cr>p

autocmd BufEnter * lcd %:p:h
let g:NERDTreeChDirMode = 2

```
# VSCODE

```
{


"version": "2.0.0",

"tasks": [

{

"label": "build",

"type": "shell",

"group": {

"kind": "build",

"isDefault": true

},

"presentation": {

"echo": true,

"reveal": "always",

"focus": false,

"panel": "shared"

},

"windows": {

"command": "g++",

"args": [

"-ggdb",

"\"${file}\"",

"--std=c++11",

"-o",

"\"${fileDirname}\\${fileBasenameNoExtension}.exe\""

]

}

}

]

}



```