
---

# docs/04-instalacion/backups.md

```md id="mxz7su"
# Política de backups

## Objetivo

Garantizar la recuperación de datos críticos.

## Backup de bases de datos

```bash
mysqldump -u root -p web_empresa > backup_web.sql