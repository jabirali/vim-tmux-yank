# Vim Tmux Yank

This is a simple plugin for synchronizing the clipboards of `vim`/`nvim`,
`tmux`, and a variety of operating systems, even over remote connections.
It does so via a little known terminal escape code known as OSC 52.

There are other ways to accomplish similar things; you can e.g. use `xclip`,
`wl-copy`, `clip.exe`, `pbcopy`. However, this requires different utilities on
different operating systems, and doesn't always work over `ssh`. Notably, many
hosts disable `X11` forwarding for security reasons, many headless servers
don't have `X11` or `xclip` installed, and Wayland or WSL users may not want an
`X` server installed just so they can get basic clipboard functionality. 
OSC 52, in contrast, works transparently over `ssh` and across platforms.

# Quickstart

This plugin assumes you use `vim` or `nvim` inside of `tmux`, and wish to synchronize
your clipboards in `tmux`, `vim`/`nvim`, and your operating system. You can
install this plugin using a standard `vim` plugin manager like `vim-plug`:

	Plug 'jabirali/vim-tmux-yank'

Then enable OSC 52 on the `tmux` side, just add this to your `~/.tmux.conf`:

	set -g set-clipboard on

This is sufficient to integrate your `vim` and `tmux` clipboards. Some terminals
like `alacritty` set your operating system clipboard by default when an OSC 52
code is intercepted, others like iTerm reportedly require you to enable this
feature in the settings. If you now yank text in `vim` (try e.g. `Vy` or `yy`),
the yanked text should be available from your `vim` clipboard, `tmux` clipboard,
and operating system clipboard. It should automatically work over `ssh` too.

# Acknowledgements

Almost all of this code was copied from [this post][1] on Reddit, so all credit
should go to that person. The only thing I did was to add `tmux` integration for
discovering your `tty`, since just setting it to `/dev/tty` didn't work for me.

I tried some existing OSC-52 plugins, and none of them seemed to work on Neovim.
According to Google, no-one else had wrapped this code as a plugin. To streamline
things for other users like me, I therefore wrapped it as a plugin myself.

[1]: https://www.reddit.com/r/vim/comments/ac9eyh/talk_i_gave_on_going_mouseless_with_vim_tmux/ed6kl67/
