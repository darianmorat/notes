# Fix: Speakers silent after suspend/resume (auto)

Speakers go silent after suspend (manual or lid-close). Fixed automatically via a systemd resume service

## Files

**`~/.local/bin/fix-audio.sh`**

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

**`/etc/sudoers.d/audio-fix`**

```
darianmorat ALL=(ALL) NOPASSWD: /usr/bin/alsaucm, /usr/bin/amixer
```

**`/etc/systemd/system/user-resume-audio.service`**

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

## Enable

```
sudo systemctl daemon-reload
sudo systemctl enable user-resume-audio.service
```
