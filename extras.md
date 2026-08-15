## Autologin at startup

```
sudo groupadd -r autologin
sudo gpasswd -a username autologin

sudo nvim /etc/lightdm/lightdm.conf
```

```
autologin-guest=false
autologin-user=username
autologin-user-timeout=0
```

## Commands for live preview on files

- https://www.npmjs.com/package/live-server
- https://www.npmjs.com/package/@mryhryki/markdown-preview

```
live-server
markdow-preview
```

## Sync data

You can use -avn instead of -avh for a dry-run and see which changes will be made beforehand  
IP changes as WiFi changes: ifconfig then check if correct `ssh -p 8022 u0_a253@192.168.XXX.X`

```
# Laptop - Mobile
rsync -avn --progress --delete -e "ssh -p 8022" ~/Documents/music/ u0_a253@192.168.XXX.X:"storage/shared/backups/music/"
```

```
# Laptop - USB
rsync -avn --progress --delete ~/Documents/music/ /run/media/darianmorat/BACKUPS/music/
sync # remember to sync after the first cmd, to remove USB safely
```

You can also sync your gdrive folder with rclone (remember to use `rclone config`)

```
rclone sync ~/path/to/local/folder gdrive:folder-name/ --dry-run --progress
rclone sync ~/path/to/local/folder gdrive:folder-name/ --progress
```

## Clean cache automatically

After installing pacman-contrib you should enable the cache cleaner:

```
sudo systemctl enable paccache.timer
```

## BIOS config

Timeout in BIOS is disabled, for showing the menu:  
Space hold - or double type for showing the other BIOS options

## Open txt files with Neovim

```
mkdir ~/.local/share/applications/
nvim ~/.local/share/applications/nvim.desktop
```

Then paste the following

```
[Desktop Entry]
Name=Neovim
Exec=wezterm start -- nvim %F
Terminal=false
Type=Application
Icon=nvim
MimeType=text/plain;
```
