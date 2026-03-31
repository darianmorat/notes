## Autologin at startup

```sh
$ sudo groupadd -r autologin
$ sudo gpasswd -a username autologin
```

```sh
$ sudo nvim /etc/lightdm/lightdm.conf
```

```
autologin-guest=false
autologin-user=username
autologin-user-timeout=0
```

## No sound after pausing

Audio stops working if you play sound, pause for 5-10s, then try
to play again. The cause is WirePlumber suspending idle ALSA nodes

Fix: disable suspension timeout in WirePlumber config

```sh
$ mkdir -p ~/.config/wireplumber/wireplumber.conf.d
$ nvim ~/.config/wireplumber/wireplumber.conf.d/51-disable-suspension.conf
```

```
monitor.alsa.rules = [
   {
      matches = [
         { node.name = "~alsa_output.*" }
      ]
      actions = {
         update-props = {
            session.suspend-timeout-seconds = 0
         }
      }
   }
]
```

## Bluetooth audio not switching automatically

Find device number under Sinks and replace X with that number

```sh
$ wpctl status
$ wpctl set-default X
```

## Don't suspend in close lid

Sound was lost when closing the lid, so the workaround is never suspending the computer
we just lock and turn off the screen instead

```sh
$ sudo nvim /etc/systemd/logind.conf
```

```
HandleLidSwitch=lock
HandleLidSwitchExternalPower=lock
```

## Commands for live preview on files

- https://www.npmjs.com/package/live-server
- https://www.npmjs.com/package/@mryhryki/markdown-preview

```sh
$ live-server
$ markdow-preview
```

## Sync data

You can use -avn instead of -avh for a dry-run and see which changes will be made beforehand  
IP changes as WiFi changes: ifconfig then check if correct `ssh -p 8022 u0_a253@192.168.XXX.X`

```sh
# Laptop - Mobile
$ rsync -avn --progress --delete -e "ssh -p 8022" ~/Documents/music/ u0_a253@192.168.XXX.X:"storage/shared/backups/music/"
```

```sh
# Laptop - USB
$ rsync -avn --progress --delete ~/Documents/music/ /run/media/darianmorat/BACKUPS/music/
$ sync # remember to sync after the first cmd, to remove USB safely
```

## Clean cache automatically

After installing pacman-contrib you should enable the cache cleaner:

```sh
$ sudo systemctl enable paccache.timer
```

## BIOS config

Timeout in BIOS is disabled, for showing the menu:  
Space hold - or double type for showing the other BIOS options

## Open txt files with Neovim

```sh
$ mkdir ~/.local/share/applications/
$ nvim ~/.local/share/applications/nvim.desktop
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
