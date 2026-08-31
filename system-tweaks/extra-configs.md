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

## BIOS config

Timeout in BIOS is disabled, for showing the menu:  
Space hold - or double type for showing the other BIOS options

## Floating Wi-Fi/Bluetooth popups

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

`~/.config/i3`

```
for_window [class="wezterm-impala"] floating enable, resize set 1920 1050, move position center
for_window [class="wezterm-bluetui"] floating enable, resize set 1920 1050, move position center
```

Check real usable area if positioning looks off:

```
i3-msg -t get_workspaces | jq '.[] | select(.focused) | .rect'
```

`~/.local/share/applications/wifi-popup.desktop`

> Rofi entries

```
[Desktop Entry]
Name=WiFi
Comment=Wi-Fi network management with Impala
Exec=/home/darianmorat/.local/bin/popup-wifi
Type=Application
Terminal=false
Icon=network-wireless
```

`~/.local/share/applications/bluetooth-popup.desktop`

```
[Desktop Entry]
Name=Bluetooth
Comment=Bluetooth device management with BlueTUI
Exec=/home/darianmorat/.local/bin/popup-bluetooth
Type=Application
Terminal=false
Icon=bluetooth
```

```
update-desktop-database ~/.local/share/applications/
```
