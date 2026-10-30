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

## App launcher entries

> Open txt files with Neovim

`~/.local/share/applications/nvim.desktop`

```
[Desktop Entry]
Name=Neovim
Exec=foot nvim %F
Icon=nvim
Comment=Vim-based text editor
Terminal=false
Type=Application
MimeType=text/plain;
```

> Add description to Seanime

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

> Add hyprpicker entry

`~/.local/share/applications/hyprpicker.desktop`

```
[Desktop Entry]
Type=Application
Name=Hyprpicker
Comment=Pick a color from the screen
Exec=hyprpicker -a
Icon=color-select
Terminal=false
Categories=Utility;
```

## Floating Wi-Fi/Bluetooth popups

`~/.local/bin/popup-wifi`

```
#!/bin/bash
foot --app-id "foot-impala" -- impala
```

`~/.local/bin/popup-bluetooth`

```
#!/bin/bash
foot --app-id "foot-bluetui" -- bluetui
```

```
chmod +x ~/.local/bin/popup-wifi ~/.local/bin/popup-bluetooth
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

## BIOS config

Timeout in BIOS is disabled, for showing the menu:  
Space hold - or double type for showing the other BIOS options.
