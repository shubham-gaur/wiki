---
title: Wiki.js Installation Guide
description: A single hand guide for self hosted wiki server
published: true
date: 2021-10-09T16:09:20.082Z
tags: guide, installation
editor: markdown
dateCreated: 2021-10-09T16:08:57.871Z
---

# Introduction

## Prerequisites

* Install postgres sql

```bahs
docker run --name postgres-db --restart unless-stopped -e POSTGRES_PASSWORD=postgres -p 5432:5432 -d postgres
```

### Backup Database
```
# generate sql:
docker exec -t your-db-container pg_dumpall -c -U your-db-user > dump_$(date +%Y-%m-%d_%H_%M_%S).sql

# to reduce the size of the sql you can generate a compress:
docker exec -t your-db-container pg_dumpall -c -U your-db-user | gzip > ./dump_$(date +"%Y-%m-%d_%H_%M_%S").gz

# restore normal sql file:
cat your_dump.sql | docker exec -i your-db-container psql -U your-db-user -d your-db-name

# restore a compressed sql:
gunzip < your_dump.sql.gz | docker exec -i your-db-container psql -U your-db-user -d your-db-name
```

## Installation

###  Using Env

* Install wiki

``` bash
docker run -d -p 8080:3000 --name wiki --restart unless-stopped -e "DB_TYPE=postgres" -e "DB_HOST=192.168.100.113" -e "DB_PORT=5432" -e "DB_USER=postgres" -e "DB_PASS=2406" -e "DB_NAME=postgres" requarks/wiki:2
```

### Using Config File

* Crete config file

```text
#######################################################################
# Wiki.js - CONFIGURATION                                             #
#######################################################################
# Full documentation + examples:
# https://docs.requarks.io/install

# ---------------------------------------------------------------------
# Port the server should listen to
# ---------------------------------------------------------------------

port: 3000

# ---------------------------------------------------------------------
# Database
# ---------------------------------------------------------------------
# Supported Database Engines:
# - postgres = PostgreSQL 9.5 or later
# - mysql = MySQL 8.0 or later (5.7.8 partially supported, refer to docs)
# - mariadb = MariaDB 10.2.7 or later
# - mssql = MS SQL Server 2012 or later
# - sqlite = SQLite 3.9 or later

db:
  type: postgres

  # PostgreSQL / MySQL / MariaDB / MS SQL Server only:
  host: 192.168.217.113
  port: 5432
  user: postgres
  pass: postgres
  db: postgres
  ssl: false

  # Optional - PostgreSQL / MySQL / MariaDB only:
  # -> Uncomment lines you need below and set `auto` to false
  # -> Full list of accepted options: https://nodejs.org/api/tls.html#tls_tls_createsecurecontext_options
  sslOptions:
    auto: true
    # rejectUnauthorized: false
    # ca: path/to/ca.crt
    # cert: path/to/cert.crt
    # key: path/to/key.pem
    # pfx: path/to/cert.pfx
    # passphrase: xyz123

  # Optional - PostgreSQL only:
  schema: public

  # SQLite only:
  storage: path/to/database.sqlite

#######################################################################
# ADVANCED OPTIONS                                                    #
#######################################################################
# Do not change unless you know what you are doing!

# ---------------------------------------------------------------------
# SSL/TLS Settings
# ---------------------------------------------------------------------
# Consider using a reverse proxy (e.g. nginx) if you require more
# advanced options than those provided below.

ssl:
  enabled: false
  port: 3443

  # Provider to use, possible values: custom, letsencrypt
  provider: custom

  # ++++++ For custom only ++++++
  # Certificate format, either 'pem' or 'pfx':
  format: pem
  # Using PEM format:
  key: path/to/key.pem
  cert: path/to/cert.pem
  # Using PFX format:
  pfx: path/to/cert.pfx
  # Passphrase when using encrypted PEM / PFX keys (default: null):
  passphrase: null
  # Diffie Hellman parameters, with key length being greater or equal
  # to 1024 bits (default: null):
  dhparam: null

  # ++++++ For letsencrypt only ++++++
  domain: wiki.yourdomain.com
  subscriberEmail: admin@example.com

# ---------------------------------------------------------------------
# Database Pool Options
# ---------------------------------------------------------------------
# Refer to https://github.com/vincit/tarn.js for all possible options

pool:
  # min: 2
  # max: 10

# ---------------------------------------------------------------------
# IP address the server should listen to
# ---------------------------------------------------------------------
# Leave 0.0.0.0 for all interfaces

bindIP: 0.0.0.0

# ---------------------------------------------------------------------
# Log Level
# ---------------------------------------------------------------------
# Possible values: error, warn, info (default), verbose, debug, silly

logLevel: info

# ---------------------------------------------------------------------
# Offline Mode
# ---------------------------------------------------------------------
# If your server cannot access the internet. Set to true and manually
# download the offline files for sideloading.

offline: false

# ---------------------------------------------------------------------
# High-Availability
# ---------------------------------------------------------------------
# Set to true if you have multiple concurrent instances running off the
# same DB (e.g. Kubernetes pods / load balanced instances). Leave false
# otherwise. You MUST be using PostgreSQL to use this feature.

ha: false

# ---------------------------------------------------------------------
# Data Path
# ---------------------------------------------------------------------
# Writeable data path used for cache and temporary user uploads.
dataPath: ./data
```

* Install wiki

```bash
docker run --rm -d -p 8080:3000 --name wiki -v /home/dietpi/docker/wiki/config.yml:/wiki/config.yml requarks/wiki:2
```