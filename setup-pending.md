## Arch

> Pending #1

Create a CMD or shortcut to set your whole computer setup. Or at least a part of it,
since right now it's a big manual config

> Pending #2

How to keep track of dotfiles/ better? some people use stow, others just run git init
on home/ but then how do u ignore all the other files that are not important? they are
too many. Search online later for a better way to keep track of those without doing
double copies like I'm currently doing + a cmd to set that up faster in a new computer,
because right now u need to copy paste every... single... file...

> Pending #3 - (JUST CHECK FAST)

zsh perfomance: `https://www.dribin.org/dave/blog/archives/2024/01/01/zsh-performance`
so I have already removed zs4h and p10k, but I would like to know if my vanilla
zsh + zsh-suggestions its actually faster, as mentioned in the post, u can use
https://github.com/romkatv/zsh-bench for benchmarks and actually see if its faster.

## Neovim

> Better IMG Preview

`https://codeberg.org/mayonster/nixos-config/src/commit/46757ff3f356d06c4207afe8a18fd9f062994390/dotfiles/nvim/lua/custom/plugins/snacks.lua`
`https://codeberg.org/mayonster/nixos-config/src/commit/46757ff3f356d06c4207afe8a18fd9f062994390/dotfiles/nvim/lua/custom/plugins/blink-icon-preview.lua`

kitty terminal, but try this in foot, in how we can get the same img preview than
this guy from theprimeagen discord channel show me. we got sixel, so is probably viable

> Shibumi.nvim

Change the names of the colors.lua to yellow and cyan... follow the names than the
terminal uses instead of the ones u see? (Is this a general thing? Should I even
care? Or just leave it the way it is? Do some research before commiting to it).

> Plugins Check

Remember to check :Tutor and :h user-manual (for user manual u type leader+e to open
the other pages so u go 1, 2, 3, 4, etc...

- mini.surround (already installed)
- mini ai - treesitter-textobjects (which one) targets.vim nvim-spider
- lazygit vs neogit / gitui / fugitive (which one is better long term, remember
  that lazygit has no way to hide the status while fetching on toggle, so is not saving
  your position - but u can use ctrl+h tho)

`https://github.com/nvim-mini/mini.nvim/discussions/243`
`https://github.com/nvim-mini/mini.nvim/blob/ff00eec0fe5e897aab3b88d3499c4eb7a8cd9ad8/doc/mini-surround.txt#L70`

## Git CLI

How to avoid the ugly wrap lazygit shows in the previewer when the text is longer than
the window? if we use side by side its gonna show the wrap icons (in cli), but when
using inline its not. Is there a way to either show the icons that indicate that its
wraped or move the text to the right where it should live (so that way it does not
break the line number from the left side).
