---
title: "Vietnamese Full-Text Search on PostgreSQL"
datePublished: Fri Nov 22 2024 02:51:21 GMT+0000 (Coordinated Universal Time)
cuid: cm3s5a52s001c09laao3dhhyh
slug: vietnamese-full-text-search-on-postgresql
tags: postgresql, full-text-search

---

### Install extensions

```bash
CREATE EXTENSION IF NOT EXISTS unaccent;
CREATE EXTENSION vector SCHEMA "public" VERSION 0.7.2;
```

### Use a custom text search configuration

```bash
CREATE TEXT SEARCH CONFIGURATION vietnamese (COPY = simple);
ALTER TEXT SEARCH CONFIGURATION vietnamese
ALTER MAPPING FOR asciiword, word
WITH unaccent, simple;
```

### Example query

```sql
SELECT staffCode, userName, staffName, phoneNumber, email
FROM public.users_embedding_table
WHERE to_tsvector('vietnamese', 
                  unaccent(COALESCE(staffCode, '') || ' ' || 
                           COALESCE(userName, '') || ' ' || 
                           COALESCE(staffName, '') || ' ' || 
                           COALESCE(phoneNumber, '') || ' ' || 
                           COALESCE(email, '')
                  )
                 ) @@ plainto_tsquery('vietnamese', unaccent('Hòa'));
```