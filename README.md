# Vim Tmux Yank

There exists a little known terminal escape code known as `OSC 52`, which lets 
terminal applications write to the clipboard. Interestingly, `tmux` supports this
escape code if you `set -g set-clipboard on` in your `~/.tmux.conf`, in which case
`tmux` can both intercept `OSC 52` codes from applications like `nvim`, and simultaneously 
forward these instructions to your terminal. If you use a terminal that supports this
escape code, this provides a simple way to synchronize the clipboards in `nvim`, `tmux`, 
and your OS. This is a plugin for `vim` and `nvim` that makes this happen.

There are other ways to accomplish similar things; you can e.g. use `xclip`, `wl-copy`,
`clip.exe`, `pbcopy`. However, this requires different utilities on different operating
systems, and doesn't always work over `ssh`. Notably, many hosts disable `X11` forwarding 
for security reasons, many headless servers don't have `X11` or `xclip` installed, and 
Wayland or WSL users may not want an `X` servers just to get a clipboard working.
`OSC 52`, in contrast, works transparently over `ssh` and across platforms.

This plugin assumes that you wish to synchronize your clipboards in `tmux`, `vim`/`nvim`,
and your operating system, and that you only use `vim`/`nvim` inside `tmux`. You
can then install it using a standard plugin manager like `vim-plug`:

	Plug 'jabirali/vim-tmux-yank'

# Acknowledgements

Almost all of this code was copied from [this post][1] on Reddit, so all credit
should go to that person. The only thing I did was to add `tmux` integration for
discovering your `tty`, since just setting it to `/dev/tty` didn't work for me.

I tried some existing OSC-52 plugins, and none of them seemed to work on Neovim.
According to Google, no-one else had wrapped this code as a plugin. To streamline
things for other users like me, I therefore wrapped it as a plugin myself.

[1]: https://www.reddit.com/r/vim/comments/ac9eyh/talk_i_gave_on_going_mouseless_with_vim_tmux/ed6kl67/
