---
title: "How to dump Postgres Database with Docker"
datePublished: Thu Jul 25 2024 15:41:25 GMT+0000 (Coordinated Universal Time)
cuid: clz1fy84y000209lccdnq7d47
slug: how-to-dump-postgres-database-with-docker
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1721922057908/292bc79c-5f1c-4617-900e-ab31d7dbb90a.jpeg
tags: postgresql, docker, tips

---

In this special case, the server doesn't have Docker installed but needs the pg\_dump command to export the database. If the pg\_dump version does not match, you get this error:

```bash
pg_dump: error: aborting because of server version mismatch
```

You can upgrade the Postgres database version, but sometimes installing the pg\_dump command does not work because the network firewall rules block the repositories.

#### The solution is here

```bash
docker pull postgres
docker run -it --rm --user root postgres bash
```

Inside the docker container, you run this command

```bash
pg_dump -h <db_hostname> -U <db_username> -f <dbname>.sql <dbname>
pg_dump -Fc -v -h <db_hostname> -U <db_username> <dbname> > <dbname>.dump
```

If the password is correct, a .sql file will be generated inside the root folder of the container. You can copy this file to the host machine with the following command:

```bash
docker cp <containerId>:/file/path/within/container /host/path/target
```