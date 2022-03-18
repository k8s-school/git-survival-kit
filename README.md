# git-survival-kit
Basic tutorial for git

## Configuration

Create and fill `$HOME/.gitconfig`:

```
[user]
	name = Your name
	email = your.email@myorg.org
[color]
	ui = auto
[alias]
    resetorigin = !git fetch origin && git reset --hard @{u} && git clean -f -d
    logfull = log --graph --decorate
    rebasemain = !git fetch origin main && git rebase -i origin/main
[push]
	default = simple
[core]
	excludesfile = ~/.gitignore_global
	editor = vim
```

## zsh users

It is recommended to use https://github.com/ohmyzsh/ohmyzsh and enable its `git` plugin in your `~/.zshrc` file, by editing the line which starts with `plugin=`

## bash users

Add some alias in your `$HOME/.bashrc`

