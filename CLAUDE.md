# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Personal Neovim configuration based on kickstart.nvim, targeting WSL2 (Ubuntu 24.04) with Neovim 0.10+. Uses lazy.nvim for plugin management.

## Architecture

- `init.lua` — Entry point. Loads core modules then bootstraps lazy.nvim with all plugin specs.
- `lua/core/options.lua` — Vim options and globals. Leader key is `<Space>`. Nerd Font is enabled (`vim.g.have_nerd_font = true`).
- `lua/core/keymaps.lua` — Global keymaps and autocommands. Includes German keyboard accommodations (`ü` for `{}`, `ß` for `()`).
- `lua/core/terminal.lua` — Floating terminal toggle (`<Space>tt` or `:Floaterminal`).
- `lua/plugins/*.lua` — Each file returns a lazy.nvim plugin spec table.

## Key conventions

- Each plugin gets its own file in `lua/plugins/` returning a single lazy.nvim spec table.
- LSP servers are configured in `lua/plugins/lsp.lua` via the `servers` table (currently `rust_analyzer` and `lua_ls`). Mason auto-installs them.
- Formatting is handled by conform.nvim with format-on-save enabled (disabled for C/C++). Lua uses `stylua`.
- Colorscheme is rose-pine with transparency enabled (Normal, CursorLine, NormalFloat backgrounds set to `none`).
- Telescope keymaps use `<leader>s` prefix for search operations; `<leader>ß` for buffer fuzzy find.

## Adding a new plugin

Create `lua/plugins/<name>.lua` returning a lazy.nvim spec, then add `require "plugins.<name>"` to the plugin list in `init.lua`.

## Adding a new LSP server

Add the server name and config to the `servers` table in `lua/plugins/lsp.lua`. Mason will auto-install it.

## Formatting

Lua files are formatted with `stylua`. Run `:ConformInfo` to check formatter status.
