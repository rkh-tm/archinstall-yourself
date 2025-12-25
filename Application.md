# Installing & Configuring Applications

> https://wiki.archlinux.org/title/List_of_applications

## JetBrainsMono Nerd Font
```bash
sudo pacman -S ttf-jetbrains-mono-nerd
```

## Firefox
Browser

## Kitty
Terminal
```bash
nvim ~/.config/kitty/kitty.conf

# font_family JetBrainsMono Nerd Font
# font_size 12.0
# enable_ligatures yes
```

### Starship
Terminal Prompt
```bash
nvim ~/.bashrc

# eval "$(starship init bash)"
```

## nwg-look
GTK theme manager

## Wofi
Application Finder

## Thunar
File manager

## zip unzip

## git
git

## VSCode
Text Editor
```bash
git clone https://aur.archlinux.org/visual-studio-code-bin.git
cd visual-studio-code-bin
makepkg -s # -s to install dependencies
pacman -U vscode_package
```

## Screenshot
```bash
sudo pacman -S grim slurp wl-clipboard
```
