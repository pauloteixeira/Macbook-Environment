# Macbook Environment

## Requirements
- Vscode Conf
- Azure Data Studio
- Homebrew
- Oh My Zsh
- Git
- Nvim
- Alacritty
- Meslo Nerd Font
- Powerlevel10k
- zsh-autosuggestions
- zsh-syntax-highlighting
- eza (better ls)
- zoxide (better cd)
- TMUX
- Config terminal initialization
- Install Terminal Warp
- Install PHP 8.3
- Install composer
- Install xDebug
- Mac Configs
- - Show battery percentage
  - Drag window with three fingers
  - Remove mount external drive icon from desktop
- Install NodeJs
- Install Yarn
- Generate SSH Key

### Add shell function to VSCode
- Press F1
- Type: shell
- Install option: Install 'code' command to PATH

### VSCode extensions
- Code Runner
- Vetur
- Dracula Official
- PHP Inteliphense
- PHP Extension Pack
- PHP Debug
- Laravel Extra Intelisense
- Prettier - Code formatter (See installations below)
- Git History
- GitLens
- Markdown Preview Enhanced
- Thunder Client
- Material Theme Icons
- Github Pullrequests (not installed at this moment)

### Install Prettier
Install Prettier and enable "format on save" Settings>Settings Type format and check the item to format when save.
In the Prettier installation screen click to go to settings and change the property "Fil code within this line limit. to 140;
![Screenshot 2024-07-14 at 17 45 35](https://github.com/user-attachments/assets/981f46ca-4b56-43ce-a038-8699edcd348e)



## Azure Data Studio
[Download](https://learn.microsoft.com/en-us/azure-data-studio/download-azure-data-studio?view=sql-server-ver16&tabs=win-install%2Cwin-user-install%2Credhat-install%2Cwindows-uninstall%2Credhat-uninstall#download-azure-data-studio) Azure Data Studio

See how to install Mysql Data Extensions [here](https://learn.microsoft.com/en-us/azure-data-studio/extensions/mysql-extension)
But you can search in the extension tab on the Azure Data Studio Editor

### Install Homebrew
```vim
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
Configure the Environment variable
```vim
$ echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
$ source ~/.zprofile
```

The seccond option is add the variable manualy into .zshrc file

### Intall Oh My Zsh
```vim
$ sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### Configure Homebrew environment variable (If not added into .zprofile file)
```vim
$ vim ~/.zshrc
```
Put the line below inside of the .zshrc file:
```vim
export PATH=/opt/homebrew/bin:$PATH
```

Run the command:
```vim
$ source ~/.zshrc
```

### Install Git
```vim
$ brew install git
```

### Install nvim
```vim
$ brew install nvim
```

### Install Alacritty
```vim
$ brew install --cask alacritty
```

### Install Meslo Nerd Font
```vim
$ brew install font-meslo-lg-nerd-font
```

## Setup Alacritty Config File
```vim
// Create config file
mkdir -p ~/.config/alacritty
cd ~/.config/alacritty

// Create config main file
touch alacritty.toml

// Open config file
nvim alacritty.toml
```

Add the follow configs to alacritty.toml file
```env
[env]
TERM = "xterm-256color"

[window]
padding.x = 10
padding.y = 10
decorations = "Buttonless"
opacity = 0.8
blur = true
option_as_alt = "Both"

[window.dimensions]
columns = 200
lines = 35

[font]
normal.family = "MesloLGS Nerd Font Mono"
size = 12
```

### Install Powerlevel10k
```vim
$ brew install powerlevel10k
```

Add to path
```vim
$ echo "source $(brew --prefix)/share/powerlevel10k/powerlevel10k.zsh-theme" >> ~/.zshrc
$ source ~/.zshrc
```

The powerlevel10k configuration wizard should show up now.

If you want to open the wizard manually do: p10k configure.

Answer the prompts to make the theme look like you would like it to. For the colors of my coolnight theme to work use either lean (with the 8 colors option) or rainbow

### Setup the colorscheme for powerlevel10k and the terminal
Now we’ll setup the colorscheme.
Navigate to ~/.config/alacritty

```vim
$ cd ~/.config/alacritty
```

Clone the Color Theme
```vim
$ git clone https://github.com/alacritty/alacritty-theme themes
```

### Add my coolnight theme to the themes folder

I’ve put together my own theme called coolnight, inspired by my previous iTerm2 theme.

You can add it to the themes directory with this command:
```vim
$ curl https://raw.githubusercontent.com/josean-dev/dev-environment-files/main/.config/alacritty/themes/themes/coolnight.toml --output ~/.config/alacritty/themes/themes/coolnight.toml
```

Now open the alacritty.toml file with your editor of choice. With Neovim it would be:
```vim
$ nvim alacritty.toml
```

Add the folowing config into alacritty.toml file
```vim
import = [
    "~/.config/alacritty/themes/themes/coolnight.toml"
]
```

The entire file have to be like the follow text
```env
import = [
	"~/.config/alacritty/themes/themes/coolnight.toml"
]

[env]
TERM = "xterm-256color"

[window]
padding.x = 10
padding.y = 10
decorations = "Buttonless"
opacity = 0.8
blur = true
option_as_alt = "Both"

[window.dimensions]
columns = 200
lines = 35

[font]
normal.family = "MesloLGS Nerd Font Mono"
size = 12
```

### Better zsh history completion with up, down arrows
Let’s improve the history completion with the up and down arrows.

Open ~/.zshrc and add the following to the bottom of this file:
```vim
# history setup
HISTFILE=$HOME/.zhistory
SAVEHIST=1000
HISTSIZE=999

setopt share_history
setopt hist_expire_dups_first
setopt hist_ignore_dups
setopt hist_verify

# completion using arrow keys (based on history)
bindkey '^[[A' history-search-backward
bindkey '^[[B' history-search-forward
```

### Setup zsh-autosuggestions plugin
```vim
$ brew install zsh-autosuggestions
$ echo "source $(brew --prefix)/share/zsh-autosuggestions/zsh-autosuggestions.zsh" >> ~/.zshrc
$ source ~/.zshrc
```

### Setup zsh-syntax-highlighting

This will provide some really nice syntax highlighting as you type out commands.

Install it like so:
```vim
$ brew install zsh-syntax-highlighting
$ echo "source $(brew --prefix)/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ~/.zshrc
$ source ~/.zshrc
```

### Install eza (better ls)
```vim
$ brew install eza
```

Create this alias in the bottom of the ~/.zshrc file
```vim
$ nvim ~/.zshrc
```
And type the content below:
```vim
# ---- Eza (better ls) -----

$ alias ls="eza --icons=always"
```

### Install zoxide (better cd)
```vim
$ brew install zoxide
```

Create this alias in the bottom of the ~/.zshrc file
```vim
$ nvim ~/.zshrc
```
And type the content below:
```vim
# ---- Zoxide (better cd) ----
$ eval "$(zoxide init zsh)"

$ alias cd="z"
```
Save and then run:
```vim
$ source ~/.zshrc
```

### Install TMUX
```vim
$ brew install tmux
```

### Config terminal initialization
```vim
# ---- Initialization term ----
if [[ $- == *i* ]]; then
        cd /Volumes/SSD-A400-480GB/Documents/www
fi

tmux
clear
```
Save and then run:
```vim
$ source ~/.zshrc
```


### Configure initialization
```vim
$ code ~/.p10k.zsh
```

Find the line:
```vim
$ typeset -g POWERLEVEL9K_INSTANT_PROMPT
```

Change the value of this variable to off:
```vim
$ typeset -g POWERLEVEL9K_INSTANT_PROMPT=off
```
Restart the Alacritty.
This line will fix the error on terminal initialization

### Install Terminal Warp
```vim
$ brew install --cask warp
```

### Install PHP
```vim
$ brew intall php@8.3
```

### Install Composer
```vim
$ brew install composer
```

### Install PHP xDebug
If xcode not installed yet run the command bellow *(Ignore php.ini xdebug entrance. Don't need it.)
```vim
$ xcode-select --install
```

With xcode installed you can install the xDebug with the command bellow
```vim
$ pecl install xdebug
```


## Mac Configs
### Show battery percebtagen
Choose Apple menu > System Settings, then click Control Center in the sidebar. 
<img width="717" alt="Screenshot 2024-07-07 at 14 26 15" src="https://github.com/pauloteixeira/Macbook-Environment/assets/144756/8c762863-f6a5-4dbc-8b54-42e2d9d854bb">

### Drag window with three fingers
- Choose Apple menu  > System Settings (or System Preferences).
- Click Accessibility.
- Click Pointer Control (or Mouse & Trackpad).
- Click the Trackpad Options button.
- Turn on “Use trackpad for dragging” (or “Enable dragging”).

### Remove mounted external drivers from desktop
- Open Finder, and click Finder next to the Apple logo.
- Choose Settings from the drop-down menu.
- Click the General tab on the Finder Settings window.
- Uncheck External disks under "Show these items on the desktop."
<img width="381" alt="Screenshot 2024-07-07 at 15 04 27" src="https://github.com/pauloteixeira/Macbook-Environment/assets/144756/e9bcfcbf-7eb9-430c-9c7f-87aa44513166">

## Install NodeJS
Verify in the [package manager page](https://nodejs.org/en/download/package-manager) how is the current LTE Version
```vim
# installs nvm (Node Version Manager)
$ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

# reload zshrc
$ source ~/.zshrc

# download and install Node.js (you may need to restart the terminal)
$ nvm install 20

# verifies the right Node.js version is in the environment
$ node -v # should print `v20.15.0`

# verifies the right NPM version is in the environment
$ npm -v # should print `10.7.0`
```

## Install Yarn
```vim
$ npm install --global yarn
```

## Generate SSH Key
```vim
$ ssh-keygen -t rsa -b 4096 -C "youremail@gmail.com"
```


You’re Done!! 🚀
