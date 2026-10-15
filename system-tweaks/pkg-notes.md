## File preview

- https://www.npmjs.com/package/live-server
- https://www.npmjs.com/package/@mryhryki/markdown-preview

## Safeeyes tweaks

Settings:

- Strick break [- enabled -]

Plugins:

- Tray icon [disabled]
- Smart pause [- enabled -]
- Screensaver [disabled]
- Health statistics [disabled]
- Limit consecutive skipping [disabled]

## Sync devices

Laptop to Mobile:

> Add the `-n` flag for dry-run.
> IP can change, so use `ifconfig` then check if its working `ssh -p 8022 u0_X@IP`.

```
rsync -avh --progress --delete -e "ssh -p 8022" ~/LOCAL_PATH/ u0_X@IP:"storage/shared/FOLDER/"
```

Laptop to USB:

> Remember to `sync` after transfer is completed, to remove USB safely.

```
rsync -avn --progress --delete ~/LOCAL_PATH/ /run/media/USERNAME/FOLDER/
sync
```

## Sync GDrive

> Add the `--dry-run` flag for dry-run.
> Remember to use `rclone config` first.

```
rclone sync ~/LOCAL_PATH/ gdrive:FOLDER/ --progress
```

Just track renamed or moved files and folders with:

```
rclone sync ~/LOCAL_PATH/ gdrive:music/ --track-renames --progress
```
