## Autologin at startup

```
sudo groupadd -r autologin
sudo gpasswd -a USERNAME autologin
```

`/etc/lightdm/lightdm.conf`

```
autologin-guest=false
autologin-user=USERNAME
autologin-user-timeout=0
```

## Clean cache automatically

After installing pacman-contrib you should enable the cache cleaner:

```
sudo systemctl enable paccache.timer
```

## Open txt files with Neovim

`~/.local/share/applications/nvim.desktop`

```
[Desktop Entry]
Name=Neovim
Exec=wezterm start -- nvim %F
Terminal=false
Type=Application
Icon=nvim
MimeType=text/plain;
```

## Add description to Seanime

`~/.local/share/applications/seanime-denshi.desktop`

```
[Desktop Entry]
Name=Seanime Denshi
Exec=/usr/bin/seanime-denshi
Icon=seanime-denshi
Comment=Anime & manga media server
Type=Application
Categories=Network;Video;
Terminal=false
```

## BIOS config

Timeout in BIOS is disabled, for showing the menu:  
Space hold - or double type for showing the other BIOS options.

## Floating Wi-Fi/Bluetooth popups

> Copy the `~/.config/i3` setup first.

`~/.local/bin/popup-wifi`

```
#!/bin/bash
wezterm start --class "wezterm-impala" -- impala
```

`~/.local/bin/popup-bluetooth`

```
#!/bin/bash
wezterm start --class "wezterm-bluetui" -- bluetui
```

```
chmod +x ~/.local/bin/popup-wifi ~/.local/bin/popup-bluetooth
```

Check real usable area if positioning looks off:

```
i3-msg -t get_workspaces | jq '.[] | select(.focused) | .rect'
```

`~/.local/share/applications/wifi-popup.desktop`

```
[Desktop Entry]
Name=WiFi
Comment=Wi-Fi network management with Impala
Exec=/home/USERNAME/.local/bin/popup-wifi
Type=Application
Terminal=false
Icon=network-wireless
```

`~/.local/share/applications/bluetooth-popup.desktop`

```
[Desktop Entry]
Name=Bluetooth
Comment=Bluetooth device management with BlueTUI
Exec=/home/USERNAME/.local/bin/popup-bluetooth
Type=Application
Terminal=false
Icon=bluetooth
```

```
update-desktop-database ~/.local/share/applications/
```

# Spotlight / Zoomer - Scripts

> Copy the `~/.config/i3` setup first.

`~/.local/bin/projecteur-start.sh`

```
#!/bin/sh
PRESET="${1:-preset2}"
rm -f "${XDG_RUNTIME_DIR:-/tmp}/projecteur-zoom"
if pgrep -x projecteur >/dev/null; then
    projecteur -c quit
    while pgrep -x projecteur >/dev/null; do sleep 0.02; done
fi
projecteur >/dev/null 2>&1 &
until ss -xl | grep -q Projecteur_local_socket; do sleep 0.02; done
projecteur -c preset="$PRESET" -c spot=on
```

`~/.local/bin/projecteur-zoom.sh`

```
#!/bin/sh
F="${XDG_RUNTIME_DIR:-/tmp}/projecteur-zoom"
if [ "$1" = reset ]; then
    rm -f "$F"
    projecteur -c spot.size=32 -c zoom.factor=2
    exit
fi
cur=$(cat "$F" 2>/dev/null || echo 2)
new=$(awk -v c="$cur" -v d="$1" 'BEGIN{n=c+d; if(n<1.5)n=1.5; if(n>20)n=20; print n}')
echo "$new" > "$F"
projecteur -c zoom.factor="$new"
```
