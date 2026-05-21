
---

# docs/04-instalacion/base-de-datos.md

```md id="lzpw4l"
# Instalación base de datos

## Instalación MariaDB

```bash
sudo apt install mariadb-server -y

## Configuración de firewall con UFW
- `ufw default deny incoming`
- `ufw allow 22/tcp`   # SSH para administración
- `ufw allow 80,443/tcp`  # Web
- `ufw enable`
