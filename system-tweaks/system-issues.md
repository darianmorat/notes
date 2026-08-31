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

## Speakers silent after suspend/resume (CURRENT ISSUE)

<!-- What about this?: ~/.local/bin/fix-audio.sh -->
<!-- #!/bin/sh -->
<!-- sudo amixer -c0 sset Speaker off -->
<!-- sudo amixer -c0 sset Headphone on -->

This fix is not working after a suspend from xautolock and sound needs to be playing for it to
work the temporary solution is using the `sound-fix` cmd from `.zshrc` for now. We know the problem
is within that scope, so keep these notes for future reference with more time to fix it:

```
alias fix-sound-old='systemctl --user restart wireplumber; sleep 1; sudo alsaucm -c hw:sofessx8336 set _verb HiFi; sudo amixer -c0 sset Speaker off; sudo amixer -c0 sset Headphone on'
alias fix-sound='mpv --loop=inf --no-video --really-quiet --volume=0 /usr/share/sounds/alsa/Front_Center.wav & MPV_PID=$!; sleep 1; systemctl --user restart wireplumber; sleep 2; sudo alsaucm -c hw:sofessx8336 set _verb HiFi; sudo amixer -c0 sset Speaker off; sudo amixer -c0 sset Headphone on; sleep 1; kill $MPV_PID 2>/dev/null'
```

Speakers go silent after suspend (manual or lid-close). Fixed automatically via a systemd resume
service (or at least what I thought, keep working on this for a full fix on different scenarios)

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

## Bluetooth audio not switching automatically

Find device number under Sinks and replace X with that number

```
wpctl status
wpctl set-default X
```

## Vivaldi freezes after copying text (CURRENT ISSUE)

I still don't really know how the issue is reproduced, but copying a file such as `init.lua` which
contains 600+ lines 2 times in any text field (such a claude or chatgpt) makes the tab/browser to
completely freeze, a solution sometimes is closing the whole browser or making a full reboot
