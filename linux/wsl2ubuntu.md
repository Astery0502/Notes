# Ubuntu with wsl2 on Windows #

## Install wsl2 and Ubuntu ##
with guide everywhere  
map the capslock into esc

## zsh and oh-my-zsh ##
1. install zsh 

```bash
cat /etc/shells 
```
see my shells, if zsh not existing
```bash
sudo apt-getminstall zsh
sudo yum install zsh
```

2. install oh-my-zsh
from the web gitee source

3. identify the zshrc

4. identify the oh-my-zsh
    1. zsh-autosuggestion
    2. autojump
    3. zsh-interactive-cd from plugins inside the oh-my-zsh
    4. zsh-syntax-highlighting

## ranger ##
1. install ranger from apt
```bash
sudo apt-get install ranger
```
2. cp the configuration files into .config/ranger
```bash
ranger --copy-config=all
```
3. change the config of rc.conf
4. configure the fzf_select

## fzf ##
1. install from apt
2. in zsh, ranger, vim, neovim, and ……

## neovim ##
0. set in the zshrc (alias, EDITOR)
1. install from apt
2. copy configuration from github 
3. install the plugins

## install coc ##
1. install npm
2. install nodejs
3. update js to newest from web: using n( sudo npm install -g n)
4. sudo n stable

