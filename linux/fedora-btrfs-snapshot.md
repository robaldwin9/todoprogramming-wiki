---
title: Fedora  BTRFS Snapshots
description: 
published: true
date: 2026-06-14T17:02:52.999Z
tags: 
editor: markdown
dateCreated: 2026-06-14T16:03:24.018Z
---

# Fedora BTRFS Snapshots
Runs through process of setting system backs with BTRFS formated drive on fedora

## Create Snapshot Locations

### Root
`sudo snapper -c root create-config /`

### Home
`sudo snapper -c home create-config /home`

### Verify
```
sudo snapper list-configs
Config │ Subvolume
───────┼──────────
home   │ /home
root   │ /
```

## Setup snapshots before/after every update
`sudo dnf install python3-dnf-plugin-snapper`


## List all snap shots
`sudo snapper -c root list`
`sudo snapper -c home list`

## Create snapshot
`sudo snapper -c root create --description "Before fedora 44 upgrade"`
`sudo snapper -c home create --description "Before fedora 44 upgrade"`

## Remove snapshot
use list command to find `<num>`
`sudo snapper -c root delete <num>`
`sudo snapper -c home delete <num>`


## Btrfs Assistant(GUI)
The GUI application for managing snapshots on fedora.

### launch via cli
`sudo btrfs-assistant`

### Create snapshot
1. navigate to snapper
2. select snapshot location (snapshot config)
3. press "new" to manually create a snapshot


## Excluding directories from snapshot
snapshots cost near zero intially and only gor in size as files are changed.
If home is 60G and 500MB worth of changes happen the snapshot only uses 500MB.
You may want to exclude directories that do not change often

### Cache
```
mv ~/.cache ~/.cache-old
btrfs subvolume create ~/.cache
cp -a ~/.cache-old/. ~/.cache/
rm -rf ~/.cache-old
```

### Trash
```
rm -rf ~/.local/share/Trash
btrfs subvolume create ~/.local/share/Trash
```

### Downloads
```
mv ~/Downloads ~/Downloads-old
btrfs subvolume create ~/Downloads
cp -a ~/Downloads-old/. ~/Downloads
rm -rf ~/Downloads-old
```

### Steam
```
killall -9 steam
mv ~/.local/share/Steam ~/.local/share/Steam-old
btrfs subvolume create ~/.local/share/Steam
cp -a ~/.local/share/Steam-old/. ~/.local/share/Steam/
rm -rf ~/.local/share/Steam-old
```

### flatpak
```
 mv ~/.local/share/flatpak ~/.local/share/flatpak-old
 btrfs subvolume create ~/.local/share/flatpak
 cp -a ~/.local/share/flatpak-old/. ~/.local/share/flatpak/
 rm -rf ~/.local/share/flatpak-old
```



