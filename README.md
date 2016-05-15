# Find the command

Find-the-command is a bunch of simple command-not-found hooks, intended for using with pacman, it is primarily targeting Arch-based distros. It uses pacman functionality for searching files, introduced in 5.0 release, so there are no useless pkgfile dependencies.

For now, there are only bash and zsh hooks. I am not familiar with fish, so there's no fish support, but I'll apreciate if someone contributes to fish support.

## How does it work?

Ineractive shells have an ability to run a specified function when entered command is not found. So these hooks contain a simple function, which is run when shell fails to find any local executables in PATH, aliases and functions, matching entered command. There are both interactive hooks, which are providing installation prompt and some other useful functionality (like showing info about package), and non-interactive, which are only displaying a package (or list of packages) that provides needed command.

## Installation

	$ git clone https://aur.archlinux.org/find-the-command.git
	$ cd find-the-command
	$ makepkg -si

Alternatively, you can use yaourt:

	$ yaourt -S find-the-command

To enable it, you need to source needed file from `/usr/share/doc/find-the-command` directory. For example, to enable interactive zsh hook, you need to place the following in your `~/.zshrc`:

	source /usr/share/doc/find-the-command/ftc-interactive.zsh

It is also necessary to create pacman files database:

	# pacman -Fy

There is also systemd timer included to update pacman files database on daily basis, so you don't need to worry about it, just run once the following:

	# systemctl enable pacman-files.timer
