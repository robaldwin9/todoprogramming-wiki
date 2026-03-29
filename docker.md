---
title: Docker
description: 
published: true
date: 2025-04-11T22:09:13.861Z
tags: 
editor: markdown
dateCreated: 2025-03-24T17:00:57.969Z
---

# Docker

## Building Images

### Build Taged imange
Build an image with tag, so we can upload it to our image repository.

Command:
`docker build -t <user>/<repo>:<tag>.`

Example:
`docker build -t robaldwin/pixoo-discord-bot:1.0.0 .`

### Upoload Image to image repository

Command:
`docker push <user>/<repo>:<tag>`

Example:
`docker push robaldwin/pixoo-discord-bot:1.0.0`

Result:
https://hub.docker.com/repository/docker/robaldwin/pixoo-discord-bot/general