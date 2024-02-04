# README

This is the readme file for my dotfiles repo

## ZSH setup

Install zsh
```
sudo pacman -S zsh
```
Install oh-my-zsh
```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Configs are in *.zshrc*

To use custom prompt
```
git clone https://github.com/alejandromume/ubunly-zsh-theme.git
cd ubunly-zsh-theme
source INSTALL.sh
```
Change the prompt in *https://github.com/alejandromume/ubunly-zsh-theme.git* to:
```
PROMPT=$'%F{%(#..red)}┌──${debian_chroot:+($debian_chroot)──}(%B%F{%(#..cyan)}%n%(#..@)%m%b%F{%(#..red)})-[%B%F{green}%(6~.%-1~/…/%4~.%5~)%b%F{%(#..red)}]\n└─%B%(#.%F{yellow}#.%F{yellow}$)%b%F{reset} '
```
Finally restart zsh
## How to replicate the dotfile in new system

Clone the repo
```
git clone --bare https://github.com/govtx86/dotfiles.git $HOME/.dotfiles
```
Add the alias (in zsh shell)
```
echo "alias dotfile='/usr/bin/git --git-dir="$HOME/.dotfiles/" --work-tree="$HOME"'" >> ~/.zshrc
```
Apply the dotfiles
```
config checkout -f

config config --local status.showUntrackedFiles no
```


## Programs

### Hyprland
```
sudo pacman -S hyprland kitty nemo rofi neovim ly

sudo systemctl enable ly.service
```

The configs are in *.config/hpyr/hyprland.conf*

### Yay setup

```
git clone https://aur.archlinux.org/yay-bin.git
cd yay-bin
makepkg -si
```


### Essential Programs

```
sudo pacman -S polkit-kde-agent dunst waybar hyprpaper firefox uxplay gst-plugins-good gst-plugins-bad gst-libav gstreamer-vaapi cliphist wlogout grim slurp swaylock playerctl otf-font-awesome pavucontrol brightnessctl

yay -S xdg-desktop-portal-hyprland-git ttf-firacode-nerd
```

Make sure to change the path to wallpaper in *.config/hypr/hyprpaper.conf*

For uxplay, start avahi daemon
```
sudo systemctl start avahi-daemon
sudo systemctl enable avahi-daemon
```

Set gtk dark theme
```
yay -S adwaita-dark
yay -S numix-icon-theme-git
gsettings set org.gnome.desktop.wm.preferences theme "Adwaita-dark"
gsettings set org.gnome.desktop.interface gtk-theme "Adwaita-dark"
gsettings set org.gnome.desktop.interface icon-theme "Numix"
```
### Media apps
```
sudo pacman -S vlc gwenview
```
## Additional apps
- qbittorent - bittorrent client
- easyeffects - audio equaliser
- cava - audio visualiser

## Other system setups

### Bluetooth setup

```
sudo pacman -S blueman
```

Start and enable bluetooth
```
sudo systemctl start bluetooth.service
sudo systemctl enable bluetooth.service
```

### Fix wifi disconnected when laptop lid closes

Make a file */etc/systemd/system/lidbehaviour_override.service* (requires sudo)

Insert the following into the file
```
[Unit]
Description=Fix aeroplane mode on/off when lid opens/closes

[Service]
ExecStart=/usr/bin/setkeycodes e058 245 e057 245

[Install]
WantedBy=multi-user.target
```

Give the file execution permission
```
sudo chdmod a+x lidbehaviour_override.service
```

Run/enable the service
```
sudo systemctl daemon-reload
systemctl start lidbehaviour_override.service
systemctl enable lidbehaviour_override.service
```
