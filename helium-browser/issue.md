<!-- Edit this file with your own words later -->

# Helium/Chromium glitch on i3 workspace switch (picom)

STATUS: workaround in place, not a real fix

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

1. Disable picom XDG autostart: ~/.config/autostart/picom.desktop with
   Hidden=true
2. ~/.local/bin/helium-first: kill picom (wait until it exits), start
   helium-browser, wait for the real window (class "helium" "Helium",
   size >= 100x100; a 10x10 helper window of the same class appears
   first), then start picom -b. At i3 login uses a fixed 2s wait instead
   (HELIUM_FIXED_WAIT=2)
3. i3: exec --no-startup-id env HELIUM_FIXED_WAIT=2 ~/.local/bin/helium-first
4. ~/.local/share/applications/helium.desktop: all Exec= lines call the
   script (rofi uses it)

## Caveats

- picom now starts only through this script
- Helium relaunch / launches by other apps may bypass it (Depth 32 again)
- Depends on process name "helium" and class "helium"/"Helium"
- ~1-2s without compositing whenever Helium cold-starts
- Chrome not fixed yet; same approach should apply (not tested)

## Still to do

- Test Chrome with the same script approach
- Report upstream (Chromium tracker; picom if it turns out relevant):
  "Window glitches on workspace switch when browser starts under a
  running compositor". Include both xwininfo depth outputs, chrome://gpu,
  picom version

## Code used

`~/.config/i3/config`

```
exec --no-startup-id env HELIUM_FIXED_WAIT=2 ~/.local/bin/helium-first
```

`~/.local/bin/helium-first`

```
#!/bin/sh
if pgrep -x helium >/dev/null; then
  exec helium-browser "$@"
fi
pkill -x picom
for i in $(seq 40); do pgrep -x picom >/dev/null || break; sleep 0.05; done
helium-browser "$@" &
if [ -n "$HELIUM_FIXED_WAIT" ]; then
  sleep "$HELIUM_FIXED_WAIT"
else
  for i in $(seq 200); do
    xwininfo -root -tree 2>/dev/null | grep '("helium" "Helium")' | grep -qE ' [0-9]{3,}x[0-9]{3,}\+' && break
    sleep 0.05
  done
  sleep 0.1
fi
pgrep -x picom >/dev/null || picom -b
```

`~/.local/share/applications/helium.desktop`

```
[Desktop Entry]
Version=1.0
Name=Helium Browser
GenericName=Web Browser
Comment=Access the Internet
Exec=/home/darianmorat/.local/bin/helium-first %U
StartupNotify=true
Terminal=false
Icon=helium-browser
Type=Application
Categories=Network;WebBrowser;
MimeType=application/pdf;application/rdf+xml;application/rss+xml;application/xhtml+xml;application/xhtml_xml;application/xml;image/gif;image/jpeg;image/png;image/webp;text/html;text/xml;x-scheme-handler/http;x-scheme-handler/https;
Actions=new-window;new-private-window;

[Desktop Action new-window]
Name=New Window
Exec=/home/darianmorat/.local/bin/helium-first

[Desktop Action new-private-window]
Name=New Incognito Window
Exec=/home/darianmorat/.local/bin/helium-first --incognito
```
