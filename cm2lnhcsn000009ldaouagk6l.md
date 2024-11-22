---
title: "Deleting Secrets from a Git repository"
datePublished: Wed Oct 23 2024 09:06:45 GMT+0000 (Coordinated Universal Time)
cuid: cm2lnhcsn000009ldaouagk6l
slug: deleting-secrets-from-a-git-repository
tags: tutorial, github, tips

---

#### Step 1: Use the filter-branch command

```bash
git filter-branch --force --index-filter \
  "git rm --cached --ignore-unmatch <PATH-TO-YOUR-FILE-WITH-SENSITIVE-DATA>" \
  --prune-empty --tag-name-filter cat -- --all
```

#### Step 2: Push your local changes to a remote repository

```bash
git push origin --force
```
