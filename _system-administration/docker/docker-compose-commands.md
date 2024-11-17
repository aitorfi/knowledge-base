---
layout: default
title: Docker Compose Commands CheatSheet
parent: Docker
---

# Docker Compose Commands CheatSheet

Docker
{: .label .label-blue }

Virtualization
{: .label .label-blue }

@see [Docker commands cheatsheet](../docker-commands)

## Run all the containers of the stack

- Use the `--build` flag to build the conatiners first.

```bash
docker compose up -d
```

## Build all the containers of the stack without running them

- Use the `--no-cache` to build the images without using cache memory.

```bash
docker compose build
```

## Remove all the conatiners of the stack

- Use the `--rmi local` flag to remove the local images of the removed containers.

```bash
docker compose down
```
