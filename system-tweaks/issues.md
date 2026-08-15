## No sound after pausing

Audio stops working if you play sound, pause for 5-10s, then try to play again. The cause is
WirePlumber suspending idle ALSA nodes

Fix: disable suspension timeout in WirePlumber config

```
mkdir -p ~/.config/wireplumber/wireplumber.conf.d
nvim ~/.config/wireplumber/wireplumber.conf.d/51-disable-suspension.conf
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

```
wpctl status
wpctl set-default X
```

# Fix: Speakers silent after suspend/resume (auto)

Speakers go silent after suspend (manual or lid-close). Fixed automatically via a systemd resume service

`~/.local/bin/fix-audio.sh`

```
#!/bin/sh
sleep 3
systemctl --user restart wireplumber
sleep 2
sudo alsaucm -c hw:sofessx8336 set _verb HiFi
sudo amixer -c0 sset Speaker off
sudo amixer -c0 sset Headphone on
```

```
chmod +x ~/.local/bin/fix-audio.sh
```

`/etc/sudoers.d/audio-fix`

```
darianmorat ALL=(ALL) NOPASSWD: /usr/bin/alsaucm, /usr/bin/amixer
```

`/etc/systemd/system/user-resume-audio.service`

```
[Unit]
Description=Fix audio after resume
After=suspend.target hibernate.target

[Service]
Type=oneshot
User=darianmorat
Environment=XDG_RUNTIME_DIR=/run/user/1000
ExecStart=/home/darianmorat/.local/bin/fix-audio.sh

[Install]
WantedBy=suspend.target hibernate.target
```

```
sudo systemctl daemon-reload
sudo systemctl enable user-resume-audio.service
```
