# Customize VIM for Python development (with autocomplete)

*Prepared by G. Iadarola*

This recipe was tested on Linux (Ubuntu). It is partially based on this recipe found [here](https://realpython.com/vim-and-python-a-match-made-in-heaven/).

## Optional: Install your own vim (without sudo)
YouCompleteMe requires a recent version of Vim compiled with python support (see requirements [here](https://github.com/ycm-core/YouCompleteMe/blob/master/README.md)). You can install it by  the following steps:

```bash
cd ~
mkdir vim_source
cd vim_source/
git clone https://github.com/vim/vim.git
cd vim
./configure --enable-python3interp --prefix=/home/giadarol/myvim
make 
make install
```
(here ```/home/giadarol``` is my home folder).

Add ```myvim/bin``` to your PATH, for example by adding in your .bashrc file:
```bash
export PATH=/home/giadarol/myvim/bin:$PATH
```

## Install Vundle


*Based on [this guide](https://github.com/VundleVim/Vundle.vim/blob/master/README.md)*

**Clone Vundle**
```bash
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

**Place the following content at the beginning of your ".vimrc" file** (```~/.vimrc``` - create the file if not existing):
```vim
set nocompatible              " be iMproved, required
filetype off                  " required

" set the runtime path to include Vundle and initialize
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
" alternatively, pass a path where Vundle should install plugins
"call vundle#begin('~/some/path/here')

" let Vundle manage Vundle, required
Plugin 'VundleVim/Vundle.vim'

" Keep Plugin commands between vundle#begin/end.

" All of your Plugins must be added before the following line
call vundle#end()            " required
filetype plugin indent on    " required
" To ignore plugin indent changes, instead use:
"filetype plugin on
"
" Brief help
" :PluginList       - lists configured plugins
" :PluginInstall    - installs plugins; append `!` to update or just :PluginUpdate
" :PluginSearch foo - searches for foo; append `!` to refresh local cache
" :PluginClean      - confirms removal of unused plugins; append `!` to auto-approve removal
"
" see :h vundle for more details or wiki for FAQ
" Put your non-Plugin stuff after this line
```

**Install vim plugins**
```bash
vim +PluginInstall +qall
```

## Install YouCompleteMe

*Based on [this guide](https://github.com/ycm-core/YouCompleteMe/blob/master/README.md)*

Note that cmake is required!

**Add in ".vimrc" the line**:
```
Plugin 'ycm-core/YouCompleteMe'
```
before  the line ```call vundle#end()```.

**Again install VIM plugins:**
```bash
vim +PluginInstall +qall
```
(It can take a minute or so).

**Run YCM install script**:

```bash
cd ~/.vim/bundle/YouCompleteMe
python3 install.py
```

## Some further customization

You can add the following to your ".vimrc" file:
```vim
set number
set hlsearch
syntax on

set backspace=indent,eol,start

set background=dark
set showcmd

let python_highlight_all = 1
```

## Final .vimrc configuration

For reference, the final ".vimrc" files looks like this:
```vim
set nocompatible              " be iMproved, required
filetype off                  " required

" set the runtime path to include Vundle and initialize
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
" alternatively, pass a path where Vundle should install plugins
"call vundle#begin('~/some/path/here')

" let Vundle manage Vundle, required
Plugin 'VundleVim/Vundle.vim'

" Keep Plugin commands between vundle#begin/end.

Plugin 'ycm-core/YouCompleteMe'


" All of your Plugins must be added before the following line
call vundle#end()            " required
filetype plugin indent on    " required
" To ignore plugin indent changes, instead use:
"filetype plugin on
"
" Brief help
" :PluginList       - lists configured plugins
" :PluginInstall    - installs plugins; append `!` to update or just :PluginUpdate
" :PluginSearch foo - searches for foo; append `!` to refresh local cache
" :PluginClean      - confirms removal of unused plugins; append `!` to auto-approve removal
"
" see :h vundle for more details or wiki for FAQ
" Put your non-Plugin stuff after this line

set number
set hlsearch
syntax on

set backspace=indent,eol,start

set background=dark
set showcmd

let python_highlight_all = 1
```