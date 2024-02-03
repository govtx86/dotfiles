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
sudo pacman -S hyprland kitty nemo rofi
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
sudo pacman -S polkit-kde-agent dunst waybar hyprpaper firefox uxplay gst-plugins-good gst-plugins-bad gst-libav gstreamer-vaapi cliphist wlogout grim slurp swaylock playerctl otf-font-awesome
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
gsettings set org.gnome.desktop.wm.preferences theme "Adwaita-dark"
```
