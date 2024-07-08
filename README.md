# Macbook Environment

## Requirements
- Vscode Conf
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
- Install PHP 8.3
- Mac Configs
- - Show battery percentage
  - Drag window with three fingers
  - Remove mount external drive icon from desktop
- Install NodeJs
- Generate SSH Key

### Add shell function to VSCode
- Press F1
- Type: shell
- Install option: Install 'code' command to PATH

### VSCode extensions
- Code Runner
- Dracula Official
- PHP Inteliphense
- PHP Extension Pack
- PHP Debug
- Laravel Extra Intelisense
- Prettier - Code formatter (See installations below)
- Git History
- GitLens
- Markdown Preview Enhanced

### Install Prettier
Install Prettier and enable "format on save" Settings>Settings Type format and check the item to format when save.
In your projects create some file .eslintrc.json and past the configurations below:
```json
{
    "extends": ["airbnb", "prettier", "plugin:node/recommended"],
    "plugins": ["prettier"],
    "rules": {
        "prettier/prettier": "error",
        "no-unused-vars": "warn",
        "no-console": "off",
        "func-names": "off",
        "no-process-exit": "off",
        "object-shorthand": "off"
    }
}
```


### Install Homebrew
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
Configure the Environment variable
```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
source ~/.zprofile
```

The seccond option is add the variable manualy into .zshrc file

### Intall Oh My Zsh
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### Configure Homebrew environment variable (If not added into .zprofile file)
```bash
vim ~/.zshrc
export PATH=/opt/homebrew/bin:$PATH
source ~/.zshrc
```

### Install Git
```bash
brew install git
```

### Install nvim
```bash
brew install nvim
```

### Install Alacritty
```bash
brew install --cask alacritty
```

### Install Meslo Nerd Font
```bash
brew install font-meslo-lg-nerd-font
```

## Setup Alacritty Config File
```bash
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
```bash
brew install powerlevel10k
```

Add to path
```bash
echo "source $(brew --prefix)/share/powerlevel10k/powerlevel10k.zsh-theme" >> ~/.zshrc
source ~/.zshrc
```

The powerlevel10k configuration wizard should show up now.

If you want to open the wizard manually do: p10k configure.

Answer the prompts to make the theme look like you would like it to. For the colors of my coolnight theme to work use either lean (with the 8 colors option) or rainbow

### Setup the colorscheme for powerlevel10k and the terminal
Now we’ll setup the colorscheme.
Navigate to ~/.config/alacritty

```bash
cd ~/.config/alacritty
```

Clone the Color Theme
```bash
git clone https://github.com/alacritty/alacritty-theme themes
```

### Add my coolnight theme to the themes folder

I’ve put together my own theme called coolnight, inspired by my previous iTerm2 theme.

You can add it to the themes directory with this command:
```bash
curl https://raw.githubusercontent.com/josean-dev/dev-environment-files/main/.config/alacritty/themes/themes/coolnight.toml --output ~/.config/alacritty/themes/themes/coolnight.toml
```

Now open the alacritty.toml file with your editor of choice. With Neovim it would be:
```bash
nvim alacritty.toml
```

Add the folowing config into alacritty.toml file
```bash
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
```ènv
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
```bash
brew install zsh-autosuggestions
echo "source $(brew --prefix)/share/zsh-autosuggestions/zsh-autosuggestions.zsh" >> ~/.zshrc
source ~/.zshrc
```

### Setup zsh-syntax-highlighting

This will provide some really nice syntax highlighting as you type out commands.

Install it like so:
```bash
brew install zsh-syntax-highlighting
echo "source $(brew --prefix)/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ~/.zshrc
source ~/.zshrc
```

### Install eza (better ls)
```bash
brew install eza
```

Create this alias in the bottom of the ~/.zshrc file
```bash
nvim ~/.zshrc
```
And type the content below:
```bash
# ---- Eza (better ls) -----

alias ls="eza --icons=always"
```

### Install zoxide (better cd)
```bash
brew install zoxide
```
Create this alias in the bottom of the ~/.zshrc file
```bash
nvim ~/.zshrc
```
And type the content below:
```bash
# ---- Zoxide (better cd) ----
eval "$(zoxide init zsh)"

alias cd="z"
```

Save and then run:
```bash
source ~/.zshrc
```


### Configure initialization
```bash
code ~/.p10k.zsh
```

Find the line:
```bash
 typeset -g POWERLEVEL9K_INSTANT_PROMPT
```

Change the value of this variable to off:
```bash
typeset -g POWERLEVEL9K_INSTANT_PROMPT=off
```
Restart the Alacritty.
This line will fix the error on terminal initialization

### Install TMUX
```bash
brew install tmux
```

### Install PHP
```bash
brew intall php@8.3
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
```bash
# installs nvm (Node Version Manager)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

# reload zshrc
source ~/.zshrc

# download and install Node.js (you may need to restart the terminal)
nvm install 20

# verifies the right Node.js version is in the environment
node -v # should print `v20.15.0`

# verifies the right NPM version is in the environment
npm -v # should print `10.7.0`
```

## Generate SSH Key
```bash
ssh-keygen -t rsa -b 4096 -C "pauloaugustot@gmail.com"
``


You’re Done!! 🚀
