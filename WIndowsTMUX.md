# Windows TMUX Configuration
## MYSYS2 Installation
Download the installer: [msys2-x86_64-20240507.exe](https://github.com/msys2/msys2-installer/releases/download/2024-05-07/msys2-x86_64-20240507.exe)

In the MYSYS2 you will probably want to install some tools like the mingw-w64 GCC to start compiling projects. Run the following command:
```vim
$ pacman -S mingw-w64-ucrt-x86_64-gcc
```
The terminal window will show the output as below. Press 'Enter' to continue:
```vim
resolving dependencies...
looking for conflicting packages...

Packages (15) mingw-w64-ucrt-x86_64-binutils-2.41-2
            mingw-w64-ucrt-x86_64-crt-git-11.0.0.r216.gffe883434-1
            mingw-w64-ucrt-x86_64-gcc-libs-13.2.0-2  mingw-w64-ucrt-x86_64-gmp-6.3.0-2
            mingw-w64-ucrt-x86_64-headers-git-11.0.0.r216.gffe883434-1
            mingw-w64-ucrt-x86_64-isl-0.26-1  mingw-w64-ucrt-x86_64-libiconv-1.17-3
            mingw-w64-ucrt-x86_64-libwinpthread-git-11.0.0.r216.gffe883434-1
            mingw-w64-ucrt-x86_64-mpc-1.3.1-2  mingw-w64-ucrt-x86_64-mpfr-4.2.1-2
            mingw-w64-ucrt-x86_64-windows-default-manifest-6.4-4
            mingw-w64-ucrt-x86_64-winpthreads-git-11.0.0.r216.gffe883434-1
            mingw-w64-ucrt-x86_64-zlib-1.3-1  mingw-w64-ucrt-x86_64-zstd-1.5.5-1
            mingw-w64-ucrt-x86_64-gcc-13.2.0-2

Total Download Size:    49.38 MiB
Total Installed Size:  418.82 MiB

:: Proceed with installation? [Y/n]
[... downloading and installation continues ...]
```

Now you can call ```gcc``` to build software for Windows.
```vim
$ gcc --version
gcc.exe (Rev2, Built by MSYS2 project) 13.2.0
```
Upgrade the pacman:
```vim
$ pacman -Syu
$ pacman -Su
```

After installing MSYS2 it will update itself via pacman, see the update guide for more information.

## TMUX INSTALLATION
Install tmux using the following command: 
```VIM
pacman -S tmux
```

## INSTALL GIT
```VIM
pacman -S git
```

## INSTALL FONTS
Download this font: [MesloLGS Nerd Font Mono](https://github.com/ryanoasis/nerd-fonts/releases/download/v3.2.1/Meslo.zip) and install then

With the right click on top of the terminal windows, you can configure the fonts

## INSTALL ZSH
```vim
$ sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

## INSTALL POWERLEVEL10K THEME
Download the theme powerlevel10k to the directory: ```/c/msys64/home/paulo.teixeira/.oh-my-zsh/themes/```
```vim
$ git clone https://github.com/romkatv/powerlevel10k.git
```

On the ```.zshrc``` file change the theme:
```vim
ZSH_THEME="powerlevel10k/powerlevel10k"
```

Run the p10k configuration:
```vim
$ zsh
```

## INSTALL PLUGINS
```VIM
$ git clone https://github.com/zsh-users/zsh-autosuggestions /c/msys64/home/paulo.teixeira/.oh-my-zsh/custom/plugins/zsh-autosuggestions
$ git clone https://github.com/zsh-users/zsh-syntax-highlighting.git /c/msys64/home/paulo.teixeira/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting
```
In the .zshrc file change the plugin line to:
```vim
plugins=(
	git
	zsh-autosuggestions
	zsh-syntax-highlighting
)
```

In the bottom of the .zshrc file put this lines:
```vim
# Verifica se o terminal é interativo antes de iniciar tmux
bash zsh
if [[ $- == *i* ]]; then
  tmux
  cd /c/Users/paulo.teixeira/Documents
  clear
fi
```

All it's done!

