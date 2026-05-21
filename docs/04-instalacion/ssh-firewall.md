
---

# docs/04-instalacion/ssh-firewall.md

```md id="t7jnsg"
# Configuración SSH y firewall

## Instalación SSH

```bash
sudo apt install openssh-server -y

## Configuración de firewall con UFW
- `ufw default deny incoming`
- `ufw allow 22/tcp`   # SSH para administración
- `ufw allow 80,443/tcp`  # Web
- `ufw enable`
