## WezTerm blank screen

It shows a small blank screen for a fraction of a second, when changing workspaces or
opening the app, I think is for the 32 depth from `xwininfo | grep -i depth`, so finding
a way to make wezterm 24 instead of 32 like kitty terminal or xterm, if none of that works
using somethig like tmux inside a terminal that has 24 bit could be a good option its not
a big problem but I keep the comment for future Reference

Dunst notifications also show a weird black bg shadow like when using it, but its not
all the time, but its happening after the screen tearing fix, same as wezterm lol, so yeah

## Bad font rendering on website

> Check this, helium is a different browser. To confirm if we can remove it
> Is this a browser issue? check Chrome and Firefox based browsers to confirm.

Apparently I need to have a `~/.config/fontconfig/fonts.conf` file to fix the
Monospace/Consolas font issue on GitHub or any other website that uses Mono fonts? Do
more research on how it works.

```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
   <match target="pattern">
      <test qual="any" name="family">
         <string>Consolas</string>
      </test>
      <edit name="family" mode="assign" binding="strong">
         <string>Noto Sans Mono</string>
      </edit>
   </match>

   <match target="pattern">
      <test qual="any" name="family">
         <string>ui-monospace</string>
      </test>
      <edit name="family" mode="assign" binding="strong">
         <string>Noto Sans Mono</string>
      </edit>
   </match>
</fontconfig>
```
