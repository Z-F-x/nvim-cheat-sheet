d# nvim-cheat-sheet
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

## Setup for autocomplete toggle hotkey of autocomplete suggestion dropdown menu
Go to `~/.config/nvim/lua/plugins`
Create a new file called `cmp.lua` if you haven't already.
Enter this into the file: 
`return {`\
`  "hrsh7th/nvim-cmp",`

`  opts = {`\
`    completion = {},`\
`  },`\
`}`

Remove `autocomplete = false` if present

Go to `~/.config/nvim` and open `init.lua`
Enter this before any instance of `require("config.lazy").` 

`-- Function to toggle autocomplete`\
`function Toggle_SuggestionDropdown()`\
`    if _G.autocomplete_enabled == true then`\
`        -- Disable autocomplete`\
`        _G.autocomplete_enabled = false`\
`  end`\
`    if  _G.autocomplete_enabled == false then`\
`        -- Enable autocomplete`\
`        _G.autocomplete_enabled = true`\
`    end`\
`end`\
`-- Map the toggle function to a hotkey (e.g., <leader>s)`\
`vim.api.nvim_set_keymap('n', '<leader>s', ':lua Toggle_SuggestionDropdown()<CR>', { noremap = true, silent = true })`

### Note
If you have multiple hotkey scripts like that disable or enable certain plugins this you have to keep the line `require("config.lazy").` after said scripts.

### Usage
The scripts adds `s` as an option in the `leader` hotkey menu. `leader` referes to the custom hotkey modifier key which by default is `\` and in this setup is also `\`. You can see what your `leader`-key is with pressing `shift` `+` `:` and running: `:h mapleader` in the Cmdline / Command line mode.

Hit `\` and `s` to toggle:
![image](https://github.com/user-attachments/assets/b01b8ae6-5e78-4125-aa4c-7cfd7f56e223)


## Setup for dual language support toggle hotkey
`leader` referes to the custom hotkey modifier key which by default is `\` and in this setup is also `\`. You can see what your `leader`-key is with pressing `shift` `+` `:` and running: `:h mapleader` in the Cmdline / Command line mode.

This setup is for `nb` (Norwegian Bokmål) and `nn` (Norwegian Nynorsk). Just change these values to the correct UTF-8 language code of your language. 

### Installation

`-- bootstrap lazy.nvim, LazyVim or your plugins
require("config.lazy")`

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
`-- bootstrap lazy.nvim, LazyVim or your plugins`
`require("config.lazy")`

You will be prompted to download and install language packs and suggestion packs if you don't have them. Confirm each download and installation with pressing `enter` for each prompt.

### Usage

When pressing `\` a message box will appear with all a list of your custom keybindings tied to `leader` or in this case `\`:

![image](https://github.com/user-attachments/assets/4b203ea7-3fdd-4041-b4f4-e0c7d12b0bf0)

Hit `t` for toggling between the two languages:

![image](https://github.com/user-attachments/assets/1e7bccc7-20d4-40e4-b0fe-4425cb272a1c)

## Setup for > 2 (more than two) languages 
`leader` referes to the custom hotkey modifier key which by default is `\` and in this setup is also `\`. You can see what your `leader`-key is with pressing `shift` `+` `:` and running: `:h mapleader` in the Cmdline / Command line mode.

This setup is for `nb` (Norwegian Bokmål), `nn` (Norwegian Nynorsk), and `en` (English). Just change these values to the correct UTF-8 language code of your language. You can add more languages if you want, the script cycle repeats from bottom to top (when at bottom and you run the hotkey it repeats from the top).

### Installation
Put the following in your `init.lua` file found in `~/.config/nvim`:

`— Toggle hotkey for mutliple languages `\
`-- Set default options for spell checking`\
`vim.opt.spell = true            -- Enable spell checking by default`\
`vim.opt.spelllang = { "nb" }    -- Set Norwegian Bokmål as the default spell language`

`-- Function to toggle between Norwegian Bokmål, Nynorsk, and English for spell checking`\
`function Toggle_spelllang()`\
`  local current_lang = vim.opt.spelllang:get()[1]  -- Get the current spell language`

`  if current_lang == "nb" then`\
`    vim.opt.spelllang = { "nn" }  -- Switch to Nynorsk`\
`    print("Switched to Nynorsk (nn)")`\
`  elseif current_lang == "nn" then`\
`    vim.opt.spelllang = { "en" }  -- Switch to English`\
`    print("Switched to English (en)")`\
`  else`\
`    vim.opt.spelllang = { "nb" }  -- Switch to Bokmål`\
`    print("Switched to Bokmål (nb)")`\
`  end`\
`end`

`-- Call the function on file load to ensure it's set to Bokmål initially`\
`Toggle_spelllang()`

`-- Map the function to a hotkey (for example, <leader>t to toggle)`\
`vim.api.nvim_set_keymap('n', '<leader>t', ':lua Toggle_spelllang()<CR>', { noremap = true, silent = true })`
`-- bootstrap lazy.nvim, LazyVim or your plugins`
`require("config.lazy")`

You will be prompted to download and install language packs and suggestion packs if you don't have them. Confirm each download and installation with pressing `enter` for each prompt.

### Usage

When pressing `\` a message box will appear with all a list of your custom keybindings tied to `leader` or in this case `\`:

![image](https://github.com/user-attachments/assets/bf3ff641-d661-40b6-b34d-dc0b3fdd5911)


Hit `t` for cycling between the languages:

![image](https://github.com/user-attachments/assets/c0806157-aa6f-4e6b-a697-cd67ba8101ac)



