---
title: Fedora  BTRFS Snapshots
description: 
published: true
date: 2026-06-14T16:03:24.018Z
tags: 
editor: markdown
dateCreated: 2026-06-14T16:03:24.018Z
---

# Fedora BTRFS Snapshorts
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


## Btrfs Assistant(GUI)
The GUI application for managing snapshots on fedora.

### launch via cli
`sudo btrfs-assistant`

### Create snapshot
1. navigate to snapper
2. select snapshot location (snapshot config)
3. press "new" to manually create a snapshot



