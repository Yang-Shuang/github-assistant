# ❗ 此插件已弃用，请使用 [vim-visual-multi](https://github.com/mg979/vim-visual-multi) 替代 ❗

# vim-multiple-cursors
[![Build Status](https://travis-ci.org/terryma/vim-multiple-cursors.svg?branch=master)](https://travis-ci.org/github/terryma/vim-multiple-cursors)

## 目录 (Contents)
 - [简介](#about)
 - [安装](#installation)
 - [快速入门](#quick-start)
 - [键位映射](#mapping)
 - [设置](#settings)
 - [与其他插件的交互](#interactions-with-other-plugins)
 - [高亮显示](#highlight)
 - [常见问题解答 (FAQ)](#faq)
 - [参与贡献](#contributing)
 - [鸣谢](#credit)

## 简介 (About)
[此前已有许多尝试][paradigm/vim-multicursor]、[felixr/vim-multiedit]、[hlissner/vim-multiedit]、[adinapoli/vim-markmultiple]、[AndrewRadev/multichange.vim] 试图将 Sublime Text 出色的 [多重选择][sublime-multiple-selection] 功能引入 Vim，但在我看来，它们都未能成为忠实且简洁的移植版本，既不够直观易用，也无法让现有 Vim 用户感到强大。`vim-multiple-cursors` 是又一版尝试。

### 非常适合快速重构
![Example1](assets/example1.gif?raw=true)

Vim 命令序列：`fp<C-n><C-n><C-n>cname`

### 为可视化选区中的每一行添加光标
![Example2](assets/example2.gif?raw=true)

Vim 命令序列：`vip<C-n>i"<Right><Right><Right>",<Esc>vipgJ$r]Idays = [`

### 匹配可视化选区中的字符
![Example3](assets/example3.gif?raw=true)

Vim 命令序列：`df[$r,0f,v<C-n>…<C-n>c<CR><Up><Del><Right><Right><Right><Del>`

### 使用命令匹配正则表达式
![Example4](assets/example4.gif?raw=true)

如需查看上述示例使用的按键，请参阅 [Wiki 页面](https://github.com/terryma/vim-multiple-cursors/wiki/Keystrokes-for-example-gifs)。

## 安装 (Installation)
请使用 [Pathogen]、[Vundle]、[Neobundle]、[vim-plug] 或你喜欢的 Vim 包管理器进行安装。

完整功能需要 vim 7.4 或更高版本。

### vim-plug 安装说明

1. 将以下代码块粘贴到 `~/.vimrc` 顶部。

```vim script
call plug#begin()

Plug 'terryma/vim-multiple-cursors'

call plug#end()
```

2. 启动 vim 并执行 `:PlugInstall`。

## 快速入门 (Quick Start)
### normal mode / visual mode（普通模式/可视化模式）
  * start：          `<C-n>` 开始多光标，并在匹配处添加一个 _虚拟光标 + 选区_
    * next：         `<C-n>` 在下一个匹配处添加新的 _虚拟光标 + 选区_
    * skip：         `<C-x>` 跳过下一个匹配项
    * prev：         `<C-p>` 移除当前 _虚拟光标 + 选区_，并返回上一个匹配项
  * select all：     `<A-n>` 开始多光标并直接选中所有匹配项

你现在可以使用 **visual mode**（可视化模式）命令来修改这些 _虚拟光标 + 选区_。
例如：`c`、`s`、`I`、`A` 均可正常使用。
你也可以按 `v` 进入 **normal mode**，并在其中使用普通模式的命令。

随时按下 `<Esc>` 即可退出并返回常规 Vim 状态。

**NOTE**: 以 `g<C-n>` 开头可忽略边界匹配（行为类似 `g*` 而非 `*`）

### visual mode when multiple lines are selected（多行选中时的可视化模式）
  * start： `<C-n>` 在每一行添加 _虚拟光标_

你现在可以使用 **normal mode**（普通模式）命令来修改这些 _虚拟光标_。
例如：`ciw`。

### command（命令）
命令 `MultipleCursorsFind` 接受一个范围和一个模式（正则表达式），它会在每个匹配项的末尾创建一个 _虚拟光标_。
如果未传入范围，则默认对整个缓冲区生效。


## 键位映射 (Mapping)
如果你不喜欢插件占用你的快捷键，可以关闭默认映射并按需重新分配：
```viml
let g:multi_cursor_use_default_mapping=0

" Default mapping
let g:multi_cursor_start_word_key      = '<C-n>'
let g:multi_cursor_select_all_word_key = '<A-n>'
let g:multi_cursor_start_key           = 'g<C-n>'
let g:multi_cursor_select_all_key      = 'g<A-n>'
let g:multi_cursor_next_key            = '<C-n>'
let g:multi_cursor_prev_key            = '<C-p>'
let g:multi_cursor_skip_key            = '<C-x>'
let g:multi_cursor_quit_key            = '<Esc>'
```

**NOTE:** 请务必确保为 `g:multi_cursor_quit_key` 映射了按键，否则你将很难退出多光标模式。

## 设置 (Settings)
目前共有四个额外的全局设置可供调整：

### ```g:multi_cursor_support_imap``` (默认值: 1)
如果设置为 0，则在 _Insert_（插入）模式下将不再支持插入映射。

### ```g:multi_cursor_exit_from_visual_mode``` (默认值: 0)
如果设置为 1，在 _Visual_（可视化）模式下按下 `g:multi_cursor_quit_key` 将会退出并删除所有现有光标，直接跳过带有多光标的普通模式。

### ```g:multi_cursor_exit_from_insert_mode``` (默认值: 0)
如果设置为 1，在 _Insert_（插入）模式下按下 `g:multi_cursor_quit_key` 将会退出并删除所有现有光标，直接跳过带有多光标的普通模式。

### ```g:multi_cursor_normal_maps``` (默认值: 见下方)
`{'@': 1, 'F': 1, 'T': 1, '[': 1, '\': 1, ']': 1, '!': 1, '"': 1, 'c': 1, 'd': 1, 'f': 1, 'g': 1, 'm': 1, 'q': 1, 'r': 1, 't': 1, 'y': 1, 'z': 1, '<': 1, '=': 1, '>': 1}`

此映射中的任何键（值会被忽略）都会使多光标 _Normal_ 模式暂停以等待按键完成，就像普通 Vim 一样。否则，当多个光标激活时，在正常模式下映射的键会“无法重放”。
例如：`{'d':1}` 可使 normal-mode 命令 `dw` 在多光标模式下正常工作。

默认列表内容应适用于大多数人，除非你将操作符挂起命令（operator-pending command）的按键重新映射为非操作符挂起命令，或反之。

这些键必须手动列出，因为 Vim 没有提供自动检测哪些键会 _启动_ 映射的方法，并且尝试将运动命令（如 `j`）作为操作符挂起命令运行可能会破坏功能。

### ```g:multi_cursor_visual_maps``` (默认值: 见下方)
`{'T': 1, 'a': 1, 't': 1, 'F': 1, 'f': 1, 'i': 1}`

与 `g:multi_cursor_normal_maps` 原理相同。

### 与其他插件的交互 (Interactions with other plugins)

### ```Multiple_cursors_before/Multiple_cursors_after``` (默认值: `nothing`)

其他插件在插入模式下可能不兼容。
因此我们提供了钩子，以便在 vim-multiple-cursors 激活时禁用这些插件：

例如，如果你正在使用 [Neocomplete](https://github.com/Shougo/neocomplete.vim)，
请在你的 vimrc 中添加以下内容以防止冲突：

```viml
function! Multiple_cursors_before()
  if exists(':NeoCompleteLock')==2
    exe 'NeoCompleteLock'
  endif
endfunction

function! Multiple_cursors_after()
  if exists(':NeoCompleteUnlock')==2
    exe 'NeoCompleteUnlock'
  endif
endfunction
```

插件本身可以在 `MultipleCursorsPre` 和 `MultipleCursorsPost` 上注册 `User` 自动命令（autocommands）以实现自动集成。

### 高亮显示 (Highlight)
该插件使用 `multiple_cursors_cursor` 和 `multiple_cursors_visual` 高亮组来分别高亮虚拟光标及其可视化选区。你可以在 vimrc 中添加类似以下内容来自定义它们：

```viml
" Default highlighting (see help :highlight and help :highlight-link)
highlight multiple_cursors_cursor term=reverse cterm=reverse gui=reverse
highlight link multiple_cursors_visual Visual
```

## 常见问题解答 (FAQ)

#### **Q** 使用 <kbd>C-n</kbd> 选中单词后按下 <kbd>i</kbd> 会导致插件卡住，为什么？
**A** 当使用 <kbd>C-n</kbd> 选中单词时，插件的行为类似于在 **visual**（可视化）模式下。
一旦你按下了 <kbd>i</kbd>，仍然可以按 <kbd>I</kbd> 来插入文本。

#### **Q** 在 VIM 中 <kbd>ALT</kbd>+<kbd>n</kbd> 似乎无效，但在 gVIM 中有效，为什么？
**A** 这是一个知名的终端/Vim [问题](http://vim.wikia.com/wiki/Get_Alt_key_to_work_in_terminal)，不同终端发送 ```Alt+key``` 的方式各不相同。
尝试在 `.vimrc` 中添加以下内容并 **务必替换该字符串**：
```vim
if !has('gui_running')
  map "in Insert mode, type Ctrl+v Alt+n here" <A-n>
endif
```
或者重新映射以下变量：
```vim
g:multi_cursor_start_key
g:multi_cursor_select_all_key
```

#### **Q** 在 gVIM 中 <kbd>CTRL</kbd>+<kbd>n</kbd> 似乎无效？
**A** 尝试在你的 `~/.gvimrc` 中设置 `set selection=inclusive`

**A** 或者，当插件激活时，你可以临时禁用 _exclusive_（独占）选择模式：
```VimL
augroup MultipleCursorsSelectionFix
    autocmd User MultipleCursorsPre  if &selection ==# 'exclusive' | let g:multi_cursor_save_selection = &selection | set selection=inclusive | endif
    autocmd User MultipleCursorsPost if exists('g:multi_cursor_save_selection') | let &selection = g:multi_cursor_save_selection | unlet g:multi_cursor_save_selection | endif
augroup END
```

### **Q** deoplete 插入乱码，如何修复？
**A** 使用 `Multiple_cursors` 函数，在 vimrc 中添加以下内容：

```VimL
    func! Multiple_cursors_before()
      if deoplete#is_enabled()
        call deoplete#disable()
        let g:deoplete_is_enable_before_multi_cursors = 1
      else
        let g:deoplete_is_enable_before_multi_cursors = 0
      endif
    endfunc
    func! Multiple_cursors_after()
      if g:deoplete_is_enable_before_multi_cursors
        call deoplete#enable()
      endif
    endfunc
```

#### **Q** macOS 支持吗？
**A** 在 Mac OS 上，[MacVim](https://code.google.com/p/macvim/) 已知可以正常工作。

#### **Q** 如何用几次按键选中 `n` 个关键词？`200<C-n>` 不起作用。
**A** 你可以使用 `:MultipleCursorsFind keyword`。我在 vimrc 中配置了如下绑定：

```VimL
nnoremap <silent> <M-j> :MultipleCursorsFind <C-R>/<CR>
vnoremap <silent> <M-j> :MultipleCursorsFind <C-R>/<CR>
```

这允许你使用 `*` 搜索关键词，并通过 `Alt-j` 将搜索结果转换为光标。


## 参与贡献 (Contributing)
欢迎提交补丁和建议！开放的功能请求列表可在 [此处](https://github.com/terryma/vim-multiple-cursors/labels/pull%20request%20welcome) 查看。

### Issue 创建
开发者的时间宝贵且有限。请确保你的问题符合 [CONTRIBUTING.md](CONTRIBUTING.md) 中概述的要求。

### Pull Requests (PR)
运行测试套件需要 ruby、rake 以及 vim。提交 PR 前，请确保检查通过：
```bash
cd vim-multiple-cursors/spec/
bundle exec rake
```

### Contributors（贡献者）
这是一个社区支持的项目。以下是所有 [Contributors](https://github.com/terryma/vim-multiple-cursors/graphs/contributors) 的名单。

## 鸣谢 (Credit)
显然，本插件受 Sublime Text 的 [多重选择][sublime-multiple-selection] 功能启发，并受到 Magnar Sveen 在 Emacs 中实现的 [multiple cursors][emacs-multiple-cursors] 的鼓励。

[vim-multiple-cursors]:http://github.com/terryma/vim-multiple-cursors
[sublime-multiple-selection]:http://www.sublimetext.com/docs/2/multiple_selection_with_the_keyboard.html
[Pathogen]:http://github.com/tpope/vim-pathogen
[Vundle]:http://github.com/gmarik/vundle
[Neobundle]:http://github.com/Shougo/neobundle.vim
[vim-plug]:https://github.com/junegunn/vim-plug
[emacs-multiple-cursors]:https://github.com/magnars/multiple-cursors.el