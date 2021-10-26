---
title: Helper Commands
description: Command snippets
published: true
date: 2021-10-26T20:26:14.277Z
tags: snippets
editor: markdown
dateCreated: 2021-10-26T20:26:14.277Z
---

# Commands

## Docker

```shell
# Jupyter
docker run -p 8888:8888 --restart unless-stopped -v "${PWD}/jupyter":/home/jovyan/work jupyter/minimal-notebook

# Wiki
docker run --rm -d -p 8080:3000 --name wiki -v /home/dietpi/docker/wiki/config.yml:/wiki/config.yml requarks/wiki:2

# Postgres
docker run --name postgres-db --restart unless-stopped -e POSTGRES_PASSWORD=postgres -p 5432:5432 -d postgres
```