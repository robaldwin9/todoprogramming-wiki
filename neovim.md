---
title: Neovim
description: 
published: true
date: 2026-02-13T03:01:52.379Z
tags: 
editor: markdown
dateCreated: 2026-02-13T03:01:50.489Z
---

# neovim

## Windows Setup

1. install neovim [neovim](https://github.com/neovim/neovim])
`winget install -e --id Neovim.Neovim`

2. install [ripgrep](https://github.com/BurntSushi/ripgrep)
`winget install -e --id BurntSushi.ripgrep.MSVC`

3. create nvim directory
`mkdir $env:localappdata/nvm`

4. vmake nvim config file
`New-Item -Path $env:localappdata/init.lua -ItemType File`

5. add lua directory
`mkdir $env:localappdata/nvm/lua

6. add plugins directory
`mkdir $env:localappdata/nvm/lua/plugins`

5. Add some default config
edit  $env:localappdata/nvim/init.lua
```
vim.o.number = true              -- Show line numbers
vim.o.relativenumber = true      -- Relative line numbers
vim.o.mouse = 'a'                -- Enable mouse support
vim.o.tabstop = 4                -- 4 space tabs
vim.o.shiftwidth = 4
vim.o.expandtab = true
vim.opt.clipboard = "unnamedplus" --copy,past to from clipboard

```