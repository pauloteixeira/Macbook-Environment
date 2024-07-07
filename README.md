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

### Add shell function to VSCode
- Press F1
- Type: shell
- Install option: Install 'code' command to PATH

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
position.x = 200

[window.dimensions]
columns = 110
lines = 20

[font]
normal.family = "MesloLGS Nerd Font Mono"
size = 19
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
position.x = 200

[window.dimensions]
columns = 110
lines = 20

[font]
normal.family = "MesloLGS Nerd Font Mono"
size = 19
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
And type the content bellow:
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
And type the content bellow:
```bash
# ---- Zoxide (better cd) ----
eval "$(zoxide init zsh)"

alias cd="z"
```

Save and then run:
```bash
source ~/.zshrc
```

### Install TMUX
```bash
brew install tmux
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
This line will fix the error on terminal initialization

You’re Done!! 🚀
