# Hyprland Dotfiles

My blue and black Hyprland setup for Arch Linux/CachyOS.

## What's here

- `hypr/`: Hyprland Lua config, Hyprlock, and Lua editor settings
- `noctalia/noctalia-config.toml`: my Noctalia user config
- `noctalia/settings.toml`: saved Noctalia GUI settings
- `noctalia/noctalia-full-config.toml`: full snapshot for reference

## 1. Install

Install the apps used by my config, or edit their commands in `hyprland.lua` to match your setup.

```bash
sudo pacman -S hyprland hyprlock git xfce4-terminal thunar network-manager-applet
```

Install Noctalia from its official instructions:
https://docs.noctalia.dev/

This config uses Hyprland's Lua configuration format. Make sure your Hyprland build supports Lua config.

## 2. Download this repo

```bash
git clone https://github.com/ecoson16/Hyprland.git ~/Hyprland
```

## 3. Restore Hyprland and Hyprlock

Back up your current config, then copy mine:

```bash
[ -d ~/.config/hypr ] && cp -a ~/.config/hypr ~/.config/hypr.backup-$(date +%Y%m%d-%H%M%S)
mkdir -p ~/.config/hypr
cp -a ~/Hyprland/hypr/. ~/.config/hypr/
```

Review the config before logging out. It launches Noctalia, `nm-applet`, and `hyprpolkitagent`. It also uses Google Chrome and Prism Launcher. Install those apps or change their commands if needed.

The Hyprlock background points to `~/Pictures/wallpaper.jpg`. Put your wallpaper there or edit `hyprlock.conf`.

Reload Hyprland:

```bash
hyprctl reload
```

## 4. Restore Noctalia

For Noctalia v5+, user config goes in `~/.config/noctalia/` and GUI-managed settings go in `~/.local/state/noctalia/settings.toml`.

```bash
mkdir -p ~/.config/noctalia ~/.local/state/noctalia
cp ~/Hyprland/noctalia/noctalia-config.toml ~/.config/noctalia/config.toml
cp ~/Hyprland/noctalia/settings.toml ~/.local/state/noctalia/settings.toml
```

The full config is a snapshot for reference. Don't copy `noctalia-full-config.toml` into the active config folder as another config file.

Some settings use paths from my computer, including wallpaper and screenshot folders. Change those paths to match yours. Then validate the config:

```bash
noctalia config validate
```

## 5. Install Pixie SDDM

Theme project: https://github.com/xCaptaiN09/pixie-sddm

On Arch/CachyOS, install SDDM and the theme's Qt6 dependencies:

```bash
sudo pacman -S sddm qt6-declarative qt6-svg git
git clone https://github.com/xCaptaiN09/pixie-sddm.git ~/pixie-sddm
cd ~/pixie-sddm
sudo ./install.sh
```

Set the installed theme to `pixie`:

```bash
printf '[Theme]\nCurrent=pixie\n' | sudo tee /etc/sddm.conf.d/10-theme.conf
```

If you're currently using LightDM, switch display managers before rebooting:

```bash
sudo systemctl disable lightdm
sudo systemctl enable sddm
```

If you use a different display manager, disable that service instead of `lightdm`. Don't enable two display managers at once. You can test the theme before switching with:

```bash
sddm-greeter-qt6 --test-mode --theme /usr/share/sddm/themes/pixie
```

## Notes

- Back up existing configs before replacing them.
- Check wallpaper paths and app commands after restoring.
- Never upload passwords, tokens, private keys, or other secrets.
