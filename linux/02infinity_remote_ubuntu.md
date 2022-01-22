# from zero to setup a remote ubuntu server #

## setup the environment ##

### set key to login without password ###
see ssh.md for more details

### setup build environment ###

1. update the machine
```
sudo apt-get update
```

2. install and update all build-essential
```
sudo apt install build-essential
```

3. install neovim and load github setup  
add default editot to .bashrc  

4. install ranger and setup
```
sudo apt install ranger
ranger --copy-config=all
```
then you can setup the rc.conf and commands.py for custom use.

5. install fzf through git
```
git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf
~/.fzf/install
```

search for hidden files
```
sudo apt install silversearcher-ag
export FZF_DEFAULT_COMMAND='ag --hidden --ignore .git -g ""'
```

use fzf in ranger, check ra.md

for more details, check [jdhao's blog for fzf](https://jdhao.github.io/2018/11/05/fzf_install_use/#:~:text=By%20default%2C%20fzf%20does%20not%20search%20hidden%20files.,a%20plugin%20to%20make%20fzf%20work%20with%20it.)

6. install miniconda
7. oppotional: add conda-forge repositories.  
```
conda config --add channels conda-forge
conda config --set channel_priority strict
```

### NEOVIM V0.6 setup ###
1. Look up [Install Neovim](https://github.com/neovim/neovim/wiki/Installing-Neovim) for messages and dowload.
2. `checkhealth` and load the required packages and environments.
3. `sudo mv nvim.appimage /usr/bin/nvim` move the appimage to usr menu and nvim to run. 
4. *oppotional* modify the aliases for `nvim` to `vim` and `vi`
5. git clone the config file for neovim.
6. install rg(ripgrep) and fd; compile the file and mv under the usr/bin/
