---
title: "How to daily back up PostgreSQL into S3"
datePublished: Sat Mar 01 2025 10:35:24 GMT+0000 (Coordinated Universal Time)
cuid: cm7q2g8r0000e09l4ceqra7af
slug: how-to-daily-back-up-postgresql-into-s3
tags: postgresql, s3

---

## Create a shell bash file as shown below

```bash
#!/bin/bash
# Directory containing temporary backup files
BACKUP_DIR="~/temp_backup"

# Format for backup file names (Ex: bk_2025-03-01.tar)
FILE_NAME="bk_$(date +%Y-%m-%d).tar"
FILE_PATH="$BACKUP_DIR/$FILE_NAME"

# S3 Bucket
S3_BUCKET="s3://your-bucket-name"

# PostgreSQL
PG_HOST=localhost
PG_PORT=5432
PG_USERNAME=postgre
PG_PASSWORD=<PGPASSWORD>
DB_NAME=postgres
DB_SCHEMA_NAME=public

# Execute a database backup leveraging Docker and the `pg_dump` utility.
docker run --rm -v "$BACKUP_DIR":/temp_backup --user root postgres bash -c "PGPASSWORD=$PGPASSWORD pg_dump --verbose --host=$PG_HOST --port=$PG_PORT --username=$PG_USERNAME --format=t --encoding=UTF-8 --file /temp_backup/$FILE_NAME -n $DB_SCHEMA_NAME $DB_NAME"

# Checking the file's successful creation, then updating it in S3.
if [ -f "$FILE_PATH" ]; then
    echo "Uploading to S3..."
    aws s3 cp "$FILE_PATH" "$S3_BUCKET/$FILE_NAME"
    
    # If uploading file successfully (exit code = 0) then remove local temporary file (optional)
    if [ $? -eq 0 ]; then
        echo "Uploaded file to S3 successfully. Removing local temporary file"
        rm -f "$FILE_PATH"
    else
        echo "Failed to upload backup file to S3"
    fi
else
    echo "Could not find the backup file: $FILE_PATH"
fi
```

## Create a crontab to run daily or at any time you prefer

```bash
crontab -e
0 0 * * * /path/to/backup_script.sh >> /var/log/backup_script.log 2>&1
chmod +x /path/to/backup_script.sh
```

## Check the Crontab log

### Ubuntu/Debian

```bash
grep CRON /var/log/syslog
```

### CentOS/RedHat

```bash
grep CRON /var/log/cron
```