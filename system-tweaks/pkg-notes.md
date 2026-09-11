## File preview

- https://www.npmjs.com/package/live-server
- https://www.npmjs.com/package/@mryhryki/markdown-preview

## Safeeyes tweaks

Settings:

- Strick break [enabled]

Plugins:

- Tray icon [disabled]
- Smart pause `Set to 10s`
- Screensaver [disabled]
- Health statistics [disabled]
- Limit consecutive skipping [disabled]

## Sync devices

You can add the flag `-n` for a dry-run and see which changes will be made  
IP changes as WiFi changes: ifconfig then check if correct `ssh -p 8022 u0_a253@192.168.XXX.X`

> Laptop to Mobile:

```
rsync -avn --progress --delete -e "ssh -p 8022" ~/LOCAL_PATH/ u0_a253@192.168.XXX.X:"storage/shared/backups/music/"
```

> Laptop to USB:  
> _Note: remember to sync after the first cmd, to remove USB safely_

```
rsync -avn --progress --delete ~/LOCAL_PATH/ /run/media/USERNAME/BACKUPS/music/
sync
```

## Sync GDrive

Sync your device to gdrive. You can add the flag `--dry-run` to see which changed will be made

> Note: remember to use `rclone config`

```
rclone sync ~/LOCAL_PATH/ gdrive:folder-name/ --progress
```

You can also just track renamed or moved files and folders with:

```
rclone sync ~/LOCAL_PATH/ gdrive:music/ --track-renames --progress
```
