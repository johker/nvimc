# nvimc

Personal Neovim configuration based on kickstart.nvim, using lazy.nvim for plugin management.

## Installation on WSL2 (Ubuntu 24.04)

### 1. Install system dependencies

```sh
sudo apt install -y build-essential git unzip ripgrep make gcc xclip
```

### 2. Install Neovim 0.10+

Ubuntu 24.04's default apt package is Neovim 0.9.5, which is too old. Install a current version via the unstable PPA:

```sh
sudo add-apt-repository ppa:neovim-ppa/unstable -y
sudo apt update
sudo apt install -y neovim
```

Verify the version:

```sh
nvim --version  # should be 0.10.0 or higher
```

### 3. Clone this config

```sh
git clone https://github.com/johker/nvimc.git "${XDG_CONFIG_HOME:-$HOME/.config}"/nvim
```

### 4. Start Neovim

```sh
nvim
```

On first launch, lazy.nvim will automatically install all plugins. Wait for the sync to complete, then restart nvim.

## Plugins

| Plugin | Purpose |
|--------|---------|
| lazy.nvim | Plugin manager |
| nvim-lspconfig + mason | LSP support and automatic LSP installer |
| nvim-cmp | Autocompletion |
| telescope.nvim | Fuzzy finder |
| treesitter | Syntax highlighting |
| neo-tree | File explorer |
| gitsigns | Git decorations |
| lazygit | Git UI (requires `lazygit` installed separately) |
| harpoon | File bookmarking |
| conform.nvim | Formatting |
| nvim-dap | Debug adapter |
| lualine | Status line |
| rose-pine | Colorscheme |
| mini.nvim | Various small utilities |

## Optional dependencies

- A [Nerd Font](https://www.nerdfonts.com/) — for icons (set `vim.g.have_nerd_font = true` in `lua/core/options.lua`)
- `npm` — for TypeScript LSP servers (installed via Mason)
- `go` — for Go LSP/tools (installed via Mason)

### Installing lazygit

The `<leader>lg` keybinding requires the `lazygit` binary. Install it to `~/.local/bin`:

```sh
LAZYGIT_VERSION=$(curl -s https://api.github.com/repos/jesseduffield/lazygit/releases/latest | grep '"tag_name"' | cut -d'"' -f4 | sed 's/^v//')
curl -Lo /tmp/lazygit.tar.gz "https://github.com/jesseduffield/lazygit/releases/download/v${LAZYGIT_VERSION}/lazygit_${LAZYGIT_VERSION}_Linux_x86_64.tar.gz"
tar -xf /tmp/lazygit.tar.gz -C /tmp lazygit
mkdir -p ~/.local/bin && install /tmp/lazygit ~/.local/bin/lazygit
```
