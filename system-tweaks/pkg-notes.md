## File preview

- https://www.npmjs.com/package/live-server
- https://www.npmjs.com/package/@mryhryki/markdown-preview

## Sync devices

You can use -avn instead of -avh for a dry-run and see which changes will be made beforehand  
IP changes as WiFi changes: ifconfig then check if correct `ssh -p 8022 u0_a253@192.168.XXX.X`

> Laptop to Mobile:

```
rsync -avn --progress --delete -e "ssh -p 8022" ~/Documents/music/ u0_a253@192.168.XXX.X:"storage/shared/backups/music/"
```

> Laptop to USB:  
> _Note: remember to sync after the first cmd, to remove USB safely_

```
rsync -avn --progress --delete ~/Documents/music/ /run/media/darianmorat/BACKUPS/music/
sync
```

## Sync GDrive

Sync your device to gdrive

> Note: remember to use `rclone config`

```
rclone sync ~/path/to/local/folder gdrive:folder-name/ --dry-run --progress
rclone sync ~/path/to/local/folder gdrive:folder-name/ --progress
```
