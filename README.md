# Vim Tmux Yank

This is a simple plugin for synchronizing the clipboards of `vim`/`nvim`,
`tmux`, and a variety of operating systems, even over remote connections.
It does so via a terminal escape called OSC 52.

There are other ways to accomplish similar things; you can e.g. use `xclip`,
`wl-copy`, `clip.exe`, `pbcopy`. However, this requires different utilities on
different systems, and doesn't always work over `ssh`. Notably, many hosts 
disable X forwarding for security reasons, many headless servers don't have
X installed, and Wayland or WSL users may not want an X server just to get
basic clipboard functionality.  OSC 52, in contrast, works transparently
over `ssh` and across platforms.

# Quickstart

This plugin assumes you use `vim` or `nvim` inside of `tmux`, and wish to synchronize
your clipboards in `tmux`, `vim`/`nvim`, and your operating system. You can
install this plugin using a standard `vim` plugin manager like [`vim-plug`][3]:

	Plug 'jabirali/vim-tmux-yank'

Then enable OSC 52 on the `tmux` side, just add this to your `tmux.conf`:

	set -g set-clipboard on

This is sufficient to integrate your `vim` and `tmux` clipboards. Some terminals
like [Alacritty][2] set your operating system clipboard by default when an OSC 52
code is intercepted, others like iTerm reportedly require you to enable this
feature in the settings. If you now yank text in `vim` (try e.g. `Vy` or `yy`),
the yanked text should be available from your `vim` clipboard, `tmux` clipboard,
and operating system clipboard. It should automatically work over `ssh` too.

This plugin lets you yank to your `tmux` and system clipboards, but you cannot
paste via terminal escape codes. This is arguably a good thing: I don't mind servers
I `ssh` into writing to my clipboard, but letting them read it is a privacy concern.
Pasting content copied outside `vim` is perhaps best done using your terminal keyboard
shortcut (I map it to <kbd>Alt</kbd>+<kbd>p</kbd>).


# Acknowledgements

Almost all of this code was copied from [Leeren's post on Reddit][1], so all 
credit should go to them. The only thing I added was the `tmux tty` check.

I tried some existing OSC-52 plugins, and none of them seemed to work on Neovim.
According to Google, no-one else had wrapped this code as a plugin. To streamline
things for other users like me, I therefore wrapped it as a plugin myself.

[1]: https://www.reddit.com/r/vim/comments/ac9eyh/talk_i_gave_on_going_mouseless_with_vim_tmux/ed6kl67/
[2]: https://github.com/alacritty/alacritty
[3]: https://github.com/junegunn/vim-plug
