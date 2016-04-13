# autoconfig-mac-vimrc

I'm a front-end engineer, and also a vimer, maybe this config file is suitable for you. This file did lots of things, such as:

- installed brew if not exist.
- installed fonts
- installed colorschemes
- installed ack 
- installed all list bundle plugins, if exist, try update.
- installed YouComplete for nodejs
- and so on.

![pic](http://ww3.sinaimg.cn/large/6c0378f8gw1f2vlasl7e5j21kw0zkanh.jpg)

The `<leader>` key is `,`，use `,ne` open folders.

## Install 

First way:

- copy the bash code very below to `install.sh`
- run command `chmod +x install.sh`
- run command `./install.sh`

Second way:

```bash
git clone https://github.com/barretlee/autoconfig-mac-vimrc.git;
cd autoconfig-mac-vimrc;
chmod +x install;
./install;
```

** bash code **
```bash
#!/bin/bash
# @author Barret Lee<barret.china@gmail.com>

# tmp dir
[[ -d ~/v-tmp ]] || mkdir ~/v-tmp;

# .vimrc
cd ~/v-tmp;
[[ -d ~/v-tmp/rc ]] || git clone
https://github.com/barretlee/autoconfig-mac-vimrc.git;

# backup origin vimrc file
[[ -f ~/.vimrc-bak ]] || cp ~/.vimrc ~/.vimrc-bak;
mv ~/v-tmp/autoconfig-mac-vimrc/.vimrc ~/.vimrc;
[[ -d ~/.vim/bundle/Vundle.vim ]] || git clone
https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim;

# colors schemes
cd ~/v-tmp;
[[ -d ~/v-tmp/vim-colorschemes ]] || git clone
https://github.com/flazz/vim-colorschemes.git;
[[ -d ~/.vim/colors ]] || mv ~/v-tmp/colors ~/.vim/;

# fonts for airline
cd  ~/v-tmp;
[[ -d ~/v-tmp/fonts ]] || git clone https://github.com/powerline/fonts.git;
cd fonts;
sh ./install.sh;

if type brew > /dev/null; then
  echo "Homebrew Exists";
else
  /usr/bin/ruby -e "$(curl -fsSL
  https://raw.githubusercontent.com/Homebrew/install/master/install)";
fi;

# ack supported
brew install ack ag;

# YouCompleteMe supported
if [[ -d ~/.vim/bundle/YouCompleteMe ]]; then
  echo "YouCompleteMe Exists";
else
  git clone https://github.com/Valloric/YouCompleteMe.git
  ~/.vim/bundle/YouCompleteMe;
  cd ~/.vim/bundle/YouCompleteMe;
  # for nodejs
  ./install.py --tern-completer;
fi;

# update vim, replace the origin 
# brew install vim --override-system-vi --with-lua --HEAD;

# install vim plugins
vim +PluginInstall! +qall;

# rm tmp dir
# rm -rf ~/v-tmp;
echo "You can remove the template dir ~/v-tmp";
```
