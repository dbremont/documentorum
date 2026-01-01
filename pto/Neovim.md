> The VIM Editing Model is a modal and keyboard-centric approach to text editing, emphasizing efficient navigation, manipulation of text objects, and a wide range of single-key and multi-key commands for tasks like insertion, deletion, and text transformation.
> 

## Index

## Features

> Here is a table summarizing the key features of Vim:
> 

| **Feature** | **Description** |
| --- | --- |
| **Modes** | Vim operates in multiple modes: Normal Mode (default for navigation and commands), Insert Mode (text input), Visual Mode (text selection), and Command-Line Mode (entering commands). |
| **Navigation** | Emphasizes keyboard-based navigation using single-key commands (e.g., h, j, k, l) and advanced movements (e.g., w for word, $ for end of line). |
| **Commands** | Offers a wide range of single-key and multi-key commands for text manipulation, search, and other tasks (e.g., `dw` to delete a word, `yy` to copy a line). |
| **Text Objects and Motions** | Provides the concept of text objects (e.g., words, sentences) and motions (e.g., forward, backward) to perform complex operations (e.g., `dip` to delete the current paragraph). |
| **Registers** | Multiple registers are available for storing and manipulating text, with the default register used for most copy-and-paste operations. |
| **Macros** | Allows recording sequences of commands and keystrokes as macros for automating repetitive tasks. |
| **Plugins and Customization** | Highly extensible through plugins and configuration files, enabling users to customize Vim to suit specific needs and workflows. |
| **Modal Editing** | Keys have different meanings depending on the mode, enabling rapid text manipulation without using a mouse or complex key combinations. |
| **Buffer-Centric** | It operates on a buffer, an in-memory representation of the edited text, and can work with multiple buffers in a session. |

## Language Server

> …
> 

- https://github.com/hrsh7th/nvim-cmp
- https://neovim.io/doc/user/lsp.html
- https://github.com/neovim/nvim-lspconfig/tree/master

## How’s To’s

```bash
-- print data path
:lua print(vim.fn.stdpath("data"))
```

Trigger Completion:

> You can trigger the completion manually by pressing `<C-x><C-o>` (in Insert mode) or simply use Neovim's built-in completion features.
> 

## Package Manager

> https://github.com/folke/lazy.nvim
> 

## References

- https://github.com/neovim/neovim
- [neovim-server](https://github.com/yqlbu/neovim-server)
- [The Vim Editor](https://web.stanford.edu/class/cs107/resources/vim)
- [Navigating in a File in Vim](https://www.baeldung.com/linux/vim-navigate-file)
- [Language Server Protocol (LSP)](https://www.notion.so/Language-Server-Protocol-LSP-f3e4edb62b984f1f950fc1039762267b?pvs=21)
- https://www.vim.org/
- https://github.com/vala-lang/vala-language-server
- [Vim Anti-Patterns (sanctum.geek.nz)](https://news.ycombinator.com/item?id=12643887)
- https://github.com/jonhoo/configs/blob/master/editor/.config/nvim/init.lua
- [Learn Vim Progressively (yannesposito.com)](https://news.ycombinator.com/item?id=2936670)
- [History and Effective Use of Vim (begriffs.com)](https://news.ycombinator.com/item?id=20481512)
- [A Vim Guide for Advanced Users (thevaluable.dev)](https://news.ycombinator.com/item?id=26284618)
- [Learning VIM while playing a game (vim-adventures.com)](https://news.ycombinator.com/item?id=3877880)
- https://github.com/dbremont/configs?tab=readme-ov-file
- [How Did Vim Become So Popular? (pragmaticpineapple.com)](https://news.ycombinator.com/item?id=23689091)
- https://www.reddit.com/r/neovim/comments/y2rwcf/best_way_to_go_about_installing_lsp_today/