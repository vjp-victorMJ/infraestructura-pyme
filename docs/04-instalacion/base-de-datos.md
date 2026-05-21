
---

# docs/04-instalacion/base-de-datos.md

```md id="lzpw4l"
# Instalación base de datos

## Instalación MariaDB

```bash
sudo apt install mariadb-server -y

## Reglas UFW
- Permitir SSH solo desde IP de la oficina: `ufw allow from 192.168.1.0/24 to any port 22`
- Permitir tráfico web: `ufw allow 80/tcp` y `ufw allow 443/tcp`
