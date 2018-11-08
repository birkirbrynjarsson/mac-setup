# Mac setup and dotfiles
Tools and instructions to speed up and automate my setup after clean re-installation of MacOS

## Requirements
Clean installation of MacOS, preferably _Mojave_ as that's what it has been tested on.

## Manual setup
I've opted out of creating a script to automate the whole setup process. I enjoy going through all the steps as well as maintaining this documentation which is enforced instead.

Install the **Xcode Command Line Tools**

```bash
xcode-select --install
```

### Configure Git
Check out [creating a personal access token](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)

```bash
git config --global user.name "Birkir Brynjarsson"  
git config --global user.email "*******@gmail.com"  
git config --global github.user birkirbrynjarsson
git config --global github.token your_token_here
git config --global core.excludesfile ~/.gitignore
echo .DS_Store >> ~/.gitignore
git config --global core.editor "code -w"
git config --global color.ui true
```

### Install Applications

Install [**Homebrew**](https://brew.sh/)

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```


Clone the repository to `~/` and install applications from **Brewfile**

```bash
git clone https://github.com/birkirbrynjarsson/.setup ~/
cd ~/.setup
brew bundle
```

### SSH keys

With **1password** installed I get my **SSH-keys** from saved documents and move to `~/.ssh` and make sure permissions are correct

```bash
chmod 600 ~/.ssh/id_rsa
chmod 600 ~/.ssh/id_rsa.pub
chmod 700 ~/.ssh
```

If the public **SSH-key** has been added to [GitHub](https://github.com/settings/ssh), the connection can be tested

```bash
ssh -T git@github.com
```

### MacOS system preferences

Run `settings.sh` to apply custom preferences for Finder, Menu bar, Dock etc.

```bash
cd ~/.setup
chmod +x settings.sh
./settings.sh
```


### Awesome terminal with iTerm2, Zsh & Oh-My-Zsh

Set preferences for iTerm2

```bash
defaults write com.googlecode.iterm2.plist PrefsCustomFolder -string "~/.setup/iterm2"
defaults write com.googlecode.iterm2.plist LoadPrefsFromCustomFolder -bool true
```

Install **[Oh-My-Zsh](https://github.com/robbyrussell/oh-my-zsh)**

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

Install [**Powerlevel9**](https://github.com/bhilburn/powerlevel9k) theme

```bash
git clone https://github.com/bhilburn/powerlevel9k.git ~/.oh-my-zsh/custom/themes/powerlevel9k
```

Install custom zsh-plugins

- [zsh-**autosuggestions**](https://github.com/zsh-users/zsh-autosuggestions)
- [zsh-**completions**](https://github.com/zsh-users/zsh-completions)
- [zsh-**history-substring-search**](https://github.com/zsh-users/zsh-history-substring-search)
- [zsh-**syntax-highlighting**](https://github.com/zsh-users/zsh-syntax-highlighting)

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM}/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-completions ${ZSH_CUSTOM}/plugins/zsh-completions
git clone https://github.com/zsh-users/zsh-history-substring-search ${ZSH_CUSTOM}/plugins/zsh-history-substring-search
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM}/plugins/zsh-syntax-highlighting
```

Install **Pygments** for colorized `cat` with `ccat`

```bash
pip3 install pygments
```

Install Ruby and `colorls` for colorful `ls` with icons. Aliased to `lc` and `lcc`

```bash
rbenv install 2.5.3
rbenv global 2.5.3
gem install bundler
gem install colorls
```


### Zsh Profile

Source the ZSH profile (optionally restart Terminal/iTerm2 after creating the symlink)

```bash
ln -s ~/.setup/zshrc ~/.zshrc
source ~/.zshrc
```

### Node
Node setup

```bash
mkdir ~/.nvm
nvm install 8.12.0
nvm install 10.13.0
nvm alias default 8.12.0
nvm use default
```

## Post installation cleanup

Cleanup Brew installations

```bash
bubu
```