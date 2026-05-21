
---

# docs/06-recuperacion.md

```md id="4lsb0r"
# Recuperación ante desastres

## Objetivo

Restaurar los servicios críticos en caso de fallo.

## Escenarios contemplados

- Fallo del servidor
- Corrupción de base de datos
- Pérdida de configuración

## Recuperación de backups

```bash
mysql -u root -p web_empresa < backup_web.sql