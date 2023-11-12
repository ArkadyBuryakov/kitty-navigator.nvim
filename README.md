# NeoVim Kitty Navigator

The Motivation behind the PlugIn is to drop my TMux dependency and to move to [Kitty](https://sw.kovidgoyal.net/kitty/).
The PlugIn is inspired by [nvim-tmux-navigation](https://github.com/alexghergh/nvim-tmux-navigation) for the NeoVim part and [vim-kitty-navigator](https://github.com/knubie/vim-kitty-navigator) for the Kitten section.

## Usage

The plugIn provides the following default key mappings to move between NeoVim and Kitty Splits:

- `<ctrl-h>` → Left
- `<ctrl-j>` → Down
- `<ctrl-k>` → Up
- `<ctrl-l>` → Right

But it supports a simple interface for changing the default mappings, see [custom bindings](#custom-bindings) section below.

## Installation

### NeoVim

Just use you preferred package manager or installation method to add it to you config.

I'm using Lazy, which results into:

```lua
{
    "MunsMan/kitty-navigator.nvim"
}
```

For **Lazy Loading** on Keybinding use:

```lua
{
    "MunsMan/kitty-navigator.nvim",
    keys = {
        {"<C-h>", function()require("kitty-navigator").navigateLeft()end, desc = "Move left a Split", mode = {"n"}}
        {"<C-j>", function()require("kitty-navigator").navigateDown()end, desc = "Move down a Split", mode = {"n"}}
        {"<C-k>", function()require("kitty-navigator").navigateUp()end, desc = "Move up a Split", mode = {"n"}}
        {"<C-l>", function()require("kitty-navigator").navigateRight()end, desc = "Move right a Split", mode = {"n"}}
    }
}
```

### Kitty

To install the kitten, there are two ways:

1. Simple copy the two python files into `~/.config/kitty/`
   -  `navigate_kitty.py`
   -  `pass_keys.py`
2. Add the copy set into the build of Lazy

```lua
{
    "MunsMan/kitty-navigator.nvim"
    build = function()
        vim.fn.system("cp", "navigate_kitty.py", "~/.config/kitty")
        vim.fn.system("cp", "pass_keys.py", "~/.config/kitty")
    end
}
```

Finally, you need to add the bindings into your kitty config (`~/.config/kitty/kitty.conf`).

    map ctrl+j kitten pass_keys.py neighboring_window bottom ctrl+j
    map ctrl+k kitten pass_keys.py neighboring_window top    ctrl+k
    map ctrl+h kitten pass_keys.py neighboring_window left   ctrl+h
    map ctrl+l kitten pass_keys.py neighboring_window right  ctrl+l

## Custom Bindings

Custom Bindings can be passed as an option in NeoVim:

```lua
{
    "MunsMan/kitty-navigator.nvim"
    opts = {
        keybindings = {
            left = "<C-h>"
            down = "<C-n>"
            up = "<C-e>"
            right = "<C-l>"

        }
    }
}
```

Finally, you need to add the bindings into your kitty config (`~/.config/kitty/kitty.conf`).

    map ctrl+h kitten pass_keys.py neighboring_window bottom ctrl+h
    map ctrl+n kitten pass_keys.py neighboring_window top    ctrl+n
    map ctrl+e kitten pass_keys.py neighboring_window left   ctrl+e
    map ctrl+l kitten pass_keys.py neighboring_window right  ctrl+l
