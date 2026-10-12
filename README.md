# Hyprland Dotfiles

My Hyprland setup and config backups for CachyOS/Arch Linux.

## What's included

- `hypr/`: Hyprland Lua config and Hyprlock config
- `noctalia/`: Noctalia settings exports
- SDDM: configured separately using the Pixie theme

## Install the basics

On CachyOS/Arch:

```bash
sudo pacman -S hyprland hyprlock git
```

Install Noctalia using its official installation instructions:
https://docs.noctalia.dev/

Install Pixie SDDM theme:
https://github.com/xCaptaiN09/pixie-sddm

My Hyprland config repository:
https://github.com/ecoson16/Hyprland

## Restore Hyprland

Back up your current config first, then copy the repository's `hypr` folder into `~/.config/hypr`.

If you cloned this repository into `~/Hyprland`:

```bash
mkdir -p ~/.config/hypr
cp -a ~/.config/hypr ~/.config/hypr.backup 2>/dev/null || true
cp -a ~/Hyprland/hypr/. ~/.config/hypr/
```

Review the config before logging out. It starts Noctalia, NetworkManager's applet, and `hyprpolkitagent`. It also uses XFCE Terminal, Thunar, Google Chrome, and Prism Launcher, so install those apps or change the commands in `hyprland.lua`.

Reload Hyprland with:

```bash
hyprctl reload
```

## Restore Noctalia

Copy the preferred exported config file to Noctalia's active settings location. On current Noctalia versions, user settings are usually stored under `~/.config/noctalia/` or `~/.local/state/noctalia/`, depending on version and install. Use Noctalia's own import/config options when available, and avoid overwriting its whole configuration blindly.

The `noctalia-full-config.toml` file is a full snapshot; `noctalia-config.toml` and `settings.toml` are smaller exports. Choose one appropriate for your installed version rather than copying all three over each other.

Some settings refer to this machine's wallpaper and screenshot paths. Update those paths on another computer.

## Restore Hyprlock

The Hyprlock config is `hypr/hyprlock.conf`. It uses `~/Pictures/wallpaper.jpg` as its background, so place your wallpaper there or edit the path.

## Configure SDDM

Install Pixie SDDM using the theme project's instructions. Then configure SDDM to use it in `/etc/sddm.conf.d/` or `/etc/sddm.conf`.

Example:

```ini
[Theme]
Current=pixie-sddm
```

The theme name must match the installed directory under `/usr/share/sddm/themes/`. Keep a working alternative login method before changing your display manager.

## Notes

- These are backups, not a universal installer. Review paths and app commands before restoring.
- Do not commit passwords, private keys, authentication tokens, or other secrets.
- SDDM system config and installed themes may need root permissions.
