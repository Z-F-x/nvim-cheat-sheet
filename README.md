# nvim-cheat-sheet
Useful tricks &amp; tips for nvim problems

## How to disable autoindentation on save
Go to: `~/.config/nvim/lua/config/options.lua` 

Add at the end of the file: `vim.g.autoformat = false`

## How to disable autocomplete suggestion dropdown menu
Go to `~/.config/nvim/lua/plugins`
Create a new file called `cmp.lua`
Add the following and save to file:

`vim.cmd([[filetype plugin indent off]])`\
`    return {`\
`    "hrsh7th/nvim-cmp",`\
`   opts = {`\
`        completion = {`\
`            autocomplete = false, -- Disable automatic completion`\
`        },`\
`    },`\
`}`

## Setup for language toggle
`leader` referes to the custom hotkey modifier key which by default is `\` and in this setup is also `\`. You can see what your `leader`-key is with pressing `shift` `+` `:` and running: `:h mapleader` in the Cmdline / Command line mode.

This setup is for `nb` (Norwegian Bokmål) and `nn` (Norwegian Nynorsk). Just change these values to the correct UTF-8 language code of your language. 

### Installation
Put the following in your `init.lua` file found in `~/.config/nvim`:

`-- Set default options for spell checking`\
`vim.opt.spell = true            -- Enable spell checking by default`\
`vim.opt.spelllang = { "nb" } -- Set Norwegian Bokmål as the default spell language`


`-- Function to toggle between Norwegian Bokmål and Nynorsk for spell checking`\
`function Toggle_spelllang()`\
`  local current_lang = vim.opt.spelllang:get()[1]  -- Get the current spell language`

`  if current_lang == "nb" then`\
`    vim.opt.spelllang = { "nn" }  -- Switch to Nynorsk`\
`    print("Switched to Nynorsk (nn)")`\
`  else`\
`    vim.opt.spelllang = { "nb" }  -- Switch to Bokmål`\
`    print("Switched to Bokmål (nb)")`\
`  end`\
`end`

`-- Call the function on file load to ensure it's set to Bokmål initially`\
`Toggle_spelllang()`

`-- Map the function to a hotkey (for example, <leader>t to toggle)`\
`vim.api.nvim_set_keymap('n', '<leader>t', ':lua Toggle_spelllang()<CR>', { noremap = true, silent = true })`
