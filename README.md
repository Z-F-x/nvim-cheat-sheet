# nvim-cheat-sheet
Useful tricks &amp; tips for nvim problems

## How to disable autoindentation on save
Go to: `~/.config/nvim/lua/config/options.lua` 

Add at the end of the file: `vim.g.autoformat = false`

## How to disable autocomplete suggestion dropdown menu
Go to `~/.config/nvim/lua/plugins`
Create a new file called `cmp.lua`
Add the following and save to file:
`vim.cmd([[filetype plugin indent off]])
return {
    "hrsh7th/nvim-cmp",

    opts = {
        completion = {
            autocomplete = false, -- Disable automatic completion
        },
    },
}`
