# dotfiles

My custom configuration files managed using a git bare repository.


## About this setup
This is a much better method than simlinking everything like I used to do. Check out this article for deets: https://www.atlassian.com/git/tutorials/dotfiles

Using this method, you don't have to deal with any simlinks so you can just add files as needed that you want and keep them in the git bare repo you create.

## How to get setup on a new system

**Initialize a bare repository**

`git init --bare $HOME/.cfg`

**Create an alias so in the future we can just type `config status` or `config push` etc instead of `git`**

`alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'`

**Don't show me untracked files (you don't care about them and you don't want them to show up)**

`config config --local status.showUntrackedFiles no`

**Add this line to your .bashrc file**

`echo "alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'" >> $HOME/.bashrc`

## How to add new or changed config files

`config add .vimrc # where .vimrc can be any config file you want tracked`

`config commit -m "added vimrc"`

`config push`

## How to setup

Create alias, reload bashrc, put cfg in gitignore, clone the bare repo, checkout and dont show untracked files, then clone vundle for plugins

```bash
echo "alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'" >> ~/.bashrc
source ~/.bashrc
echo ".cfg" >> .gitignore
git clone --bare git@github.com:nancynobody/dotfiles.git .cfg/
config checkout
config config --local status.showUntrackedFiles no
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```
