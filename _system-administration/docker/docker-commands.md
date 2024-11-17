---
layout: default
title: Docker Commands CheatSheet
parent: Docker
---

# Docker Command cheatsheet

Docker
{: .label .label-blue }

Virtualization
{: .label .label-blue }

@see [Docker compose commands cheatsheet](../docker-compose-commands)

## List running containers

- Use the `-a` flag to list all container.

```bash
docker ps
```

## List images

```bash
docker images
```

## Remove images

```bash
docker rmi <image1> <image2>
```

## Open a shell inside a container

```bash
docker exec -it <container_name> bash
```

## Remove unused volumes

```bash
docker volume prune
```

## Remove unused networks

```bash
docker network prune
```

## Inspect container logs

- Use the `--follow` flag to inspect the live logs.

```bash
docker logs --details <container>
```
