# Helium/Chromium glitch on i3 workspace switch + picom

STATUS: workaround in place, not a real fix

## Versions

> Picom = v13 (/srcdest/picom revision d87a5ba)

> Helium = 0.19.3.1 (Official Build) (x86_64)

> Chromium = 155.0.8059.79 Arch Linux

## Symptom

- Switching workspaces (or stacked/tabbed windows) in Helium/Chrome shows
  a glitch/blank frame; other apps are fine
- Intermittent across reboots; killing picom alone doesn't fix it

## What I found

- Chromium picks a 32-bit ARGB window visual when a compositor (picom) is
  already running at window creation, and a 24-bit one otherwise
  (xwininfo | grep -i depth)
- Helium started under picom = Depth 32 = glitch
- Helium started first, picom after = Depth 24 = smooth
- --disable-gpu-compositing hides the glitch but leaves a blank frame
- Depth 24 isn't enough by itself: when picom restarts also matters
  (class-based wait flickered at login, fixed 2s wait didn't)
- Not the cause: picom backend (glx/xrender/egl), use-damage,
  xrender-sync-fence, rounded frame / system title bar settings
- Setup: Arch, i3, picom, Intel UHD (CometLake-U, i915), Helium + Chrome

## Workaround

`~/.config/autostart/picom.desktop`

```
[Desktop Entry]
Type=Application
Name=picom
Hidden=true
```

`~/.local/bin/helium-start`

```
#!/bin/sh
if pgrep -x helium >/dev/null; then
  exec helium-browser "$@"
fi
pkill -x picom
for i in $(seq 40); do pgrep -x picom >/dev/null || break; sleep 0.05; done
helium-browser "$@" &
sleep 2
pgrep -x picom >/dev/null || picom -b
```

`~/.config/i3/config`

```
exec --no-startup-id ~/.local/bin/helium-start
```

`~/.local/share/applications/helium.desktop`

```
[Desktop Entry]
Version=1.0
Name=Helium Browser
GenericName=Web Browser
Comment=Access the Internet
Exec=/home/darianmorat/.local/bin/helium-start %U
StartupNotify=true
Terminal=false
Icon=helium-browser
Type=Application
Categories=Network;WebBrowser;
MimeType=application/pdf;application/rdf+xml;application/rss+xml;application/xhtml+xml;application/xhtml_xml;application/xml;image/gif;image/jpeg;image/png;image/webp;text/html;text/xml;x-scheme-handler/http;x-scheme-handler/https;
Actions=new-window;new-private-window;

[Desktop Action new-window]
Name=New Window
Exec=/home/darianmorat/.local/bin/helium-start

[Desktop Action new-private-window]
Name=New Incognito Window
Exec=/home/darianmorat/.local/bin/helium-start --incognito
```

## Caveats

- picom now starts only through this script
- Helium relaunch / launches by other apps may bypass it (Depth 32 again)
- All Chromium browsers not fixed yet; same approach should apply (not tested)

## Still to do

- Test other Chromium browsers with the same script approach
- Report upstream Chromium, Picom, Helium, etc
- Re-test without the workaround on current versions before reporting
