# Configuring Hardware

## Power Management

### TLP
```bash
sudo pacman -S tlp tlp-rdw
sudo systemctl enable tlp.service
sudo systemctl enable NetworkManager-dispatcher.service
```

```bash
sudo nvim /etc/tlp.conf

DEVICES_TO_DISABLE_ON_STARTUP="bluetooth nfc wwan"
DEVICES_TO_ENABLE_ON_STARTUP="wifi"
```

### Brightness
```bash
sudo pacman -S brightnessctl
```

## Sound System
```bash
sudo pacman -S alsa-utils # alsa tools

sudo pacman -S pipewire pipewire-pulse pipewire-jack wireplumber
```

## Network
```bash
sudo pacman -S networkmanager # should already be installed

nmcli device wifi list
nmcli device wifi connect SSID_or_BSSID password password
```
