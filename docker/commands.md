---
title: Docker Commands
description: 
published: true
date: 2026-03-30T04:17:21.738Z
tags: 
editor: markdown
dateCreated: 2025-03-24T16:56:38.839Z
---

# Docker Commands
Most commonly used docker commands.

## List docker containers
`docker ps`
you can also use `watch docker ps` if you are specifically checking to see if the container is crashing.

## Compose

### Start container

#### Attatched
`docker compose up`

#### Detached
`docker compose up -d`

### Stop Container

#### Persist data
`docker compose down`

#### Clear Volumes
`docker compose down -v`

## Logs
`docker logs <conatainer-name>`

## Run Terminal Session Within Container
`docker exec -it <container-name> bash`