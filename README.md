# git-survival-kit
Basic tutorial for git

## Configuration and aliases

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

### zsh users

It is recommended to use https://github.com/ohmyzsh/ohmyzsh and enable its `git` plugin in your `~/.zshrc` file, by editing the line which starts with `plugin=`

### bash users

Add some aliases in your `$HOME/.bashrc`

```shell
# For Ubuntu
BASHRC="$HOME/.bash_aliases"
# For MacOS
BASHRC="$HOME/.bash_profile"
echo "alias ga='git add .'" >> $BASHRC
echo "alias gc='git commit'" >> $BASHRC
echo "alias gco='git checkout'" >> $BASHRC
echo "alias gg='ga . && gc -m \'Update current feature\' && gp'" >> $BASHRC
echo "alias gp='git push'" >> $BASHRC
echo "alias gst='git status'" >> $BASHRC
```

## KISS workflow

```shell
# Checkout the code for a git repository
git clone https://github.com/k8s-school/git-survival-kit.git
cd git-survival-kit
# Create a branch
gco -b <BRANCH_NAME>

## ADD A COMMIT
# Edit some files and add their content to the index
ga .
# Commit
gc -m "Add a your feature description here"
# Push your commit
gp
# For the first push you have to cut and paste the command display by git cli
git push --set-upstream origin <BRANCH_NAME>

# Loop over the "ADD A COMMIT" section until the feature implementation is completed
# or use all-in-one alias below
gg

# Then prepare merge on main branch, an easy solution is to squash your commits altogether
git rebasemain
# Eventually make a Pull/Merge Request in Github/Gitlab
# Once your PR/MR is reviewed, merge to main branch
gco main
git merge --no-ff <BRANCH_NAME>
gp
# Eventually delete your branch
git branch -d <BRANCH_NAME>
git push origin --delete <BRANCH_NAME>
```

## Tips an tricks

### Recover a screwed up repository

When working on a branch, if your local repository is screwed up, then you can try to fix it using:
```shell
# Stash your changes in a dirty working directory away
git stash
# Reset your branch to the remote one
git resetorigin
# Apply your stashed changes on top of the current working tree state
git stash pop
```

An other option is to:
- identify your change using `gst`
- then copy it to a temporary directory
- remove the repository
- clone it again
- checkout the branch
- then copy back your changes to the new repository
- use previous KISS workflow


### View commit history

```shell
# Nice view of commit history
git logfull
# View code for each commit
git log -p
```