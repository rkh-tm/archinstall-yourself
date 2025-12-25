# Setting up GUI

## GPU Drivers
```bash
sudo pacman -S mesa \ # AMD openGL
vulkan-radeon
```

## Base Desktop "Environment"
```bash
sudo pacman -S wayland \ # display server
hyprland \ # wayland compositor
waybar \ # top bar
hyprpaper \ # wallpaper
sddm \ # display manager
xdg-user-dirs \ # default directories (e.g ~/Downloads)
noto-fonts \ # basic font
kitty # terminal

sudo systemctl enable ssdm
xdg-user-dirs-update
```
