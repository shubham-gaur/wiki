---
title: Postgres Automatic Backup
description: Simple crontab task to run regular backups of postgres container
published: true
date: 2021-10-09T16:55:30.722Z
tags: backup, db
editor: markdown
dateCreated: 2021-10-09T16:21:50.926Z
---

# Backup

## Prerequisites

1. User must have docker permissions
1. Prior knowledge of cron jobs
1. Create back up directory.
	Eg. `mkdir -p /home/pi/.backups/postgres`

## Update crontab

### Available Options

Below is the list of available backup options
```
# generate sql:
docker exec -t your-db-container pg_dumpall -c -U your-db-user > dump_$(date +%Y-%m-%d_%H_%M_%S).sql
  
# to reduce the size of the sql you can generate a compress:
docker exec -t your-db-container pg_dumpall -c -U your-db-user | gzip > ./dump_$(date +"%Y-%m-%d_%H_%M_%S").gz
```

* Modify user crontab
  * Run `crontab -e`
  * Append the following lines with required modifications.
	```
	29 */2 * * * rm /home/pi/.backups/postgres/dump_*
	*/30 * * * * /usr/bin/docker exec postgres-db pg_dumpall -c -U postgres > /home/pi/.backups/postgres/dump_$(date +\%Y-\%m-\%d_\%H_\%M_\%S).sql
	```
# Verification
> Verify new task: `crontab -l`
![postgres-bckup.png](/assets/postgres-bckup.png)
{.is-success}