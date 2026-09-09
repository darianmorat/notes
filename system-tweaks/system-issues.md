## No sound after pausing

Audio stops working if you play sound, pause for 5-10s, then try to play again. The cause is
WirePlumber suspending idle ALSA nodes. Fixed disabling suspension timeout in WirePlumber config

`~/.config/wireplumber/wireplumber.conf.d/51-disable-suspension.conf`

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

## Speakers silent after suspend/resume

`~/.local/bin/fix-audio.sh`

```
#!/bin/sh
timeout 4 mpv --loop=inf --no-video --really-quiet --volume=0 /usr/share/sounds/alsa/Front_Center.wav &
systemctl --user restart wireplumber
sleep 1
sudo alsaucm -c hw:sofessx8336 set _verb HiFi
sudo amixer -c0 sset Speaker off
sudo amixer -c0 sset Headphone on
```

```
chmod +x ~/.local/bin/fix-audio.sh
```

`/etc/sudoers.d/audio-fix`

```
USERNAME ALL=(ALL) NOPASSWD: /usr/bin/alsaucm, /usr/bin/amixer
```

`/etc/systemd/system/user-resume-audio.service`

```
[Unit]
Description=Fix audio after resume
After=suspend.target hibernate.target

[Service]
Type=oneshot
User=USERNAME
Environment=XDG_RUNTIME_DIR=/run/user/1000
ExecStart=/home/USERNAME/.local/bin/fix-audio.sh

[Install]
WantedBy=suspend.target hibernate.target
```

```
sudo systemctl daemon-reload
sudo systemctl enable user-resume-audio.service
```

## Bluetooth audio not switching automatically

Find device number under Sinks and replace X with that number

```
wpctl status
wpctl set-default X
```

## Vivaldi freezes after copying text

I still don't really know how the issue is reproduced, but copying a file such as `init.lua` which
contains 600+ lines 2 times in any text field (such a claude or chatgpt) makes the tab/browser to
completely freeze, a solution sometimes is closing the whole browser or making a full reboot
